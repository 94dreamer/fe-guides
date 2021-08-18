# 项目相关

## 整体结构图

![frk](https://b.yzcdn.cn/public_files/009d915ba00f14caee38fe982410ff23.png)

## 模块导出方式

1. controller 层使用`export = BaseClass`方式导出，原因是 astroboy 目前只支持 commonjs 方式引入
2. 只被 ts 模块引用的模块可用 es6 的方式导出：`export default BaseClass`;
3. 在切 TS 过渡过程中，会存在一个模块既被 TS 模块和 JS 模块引用，那么这个模块需通过`export = BaseClass`方式导出

实例代码：

```js
export = class LoggerController extends BaseController {}
```

## 类型定义共享

> 目的是实现 node、client 层接口交互类型校验的一致性

- `definitions`根目录下放共享的类型定义；
- `app/definitions`和`client/definitions`分别放各端的类型定义；

## client 层规范

`js`文件全部改成`ts`，补全 ts 定义；

### vue 文件书写方式

`script`标签加上`lang`属性即可，如下：

```js
<script lang="ts">
<script>
```

PS：打包工具内部通过`@babel/plugin-transform-typescript`插件实现了 vue 内部 ts 编译

# 具体规范

目前我们使用的规范是基于`@xxx/koko/node`并在商品项目添加了更严格的一层规则。

## 可以明确定义的类型不能使用 any

```js
// 错误
const age: any = "seventeen";
const ages: any[] = ["seventeen"];
const ages: Array<any> = ["seventeen"];
function greet(): any {}
function greet(): any[] {}
function greet(): Array<any> {}
function greet(): Array<Array<any>> {}
function greet(param: Array<any>): string {}
function greet(param: Array<any>): Array<any> {}

// 正确
const age: number = 17;
const ages: number[] = [17];
const ages: Array<number> = [17];
function greet(): string {}
function greet(): string[] {}
function greet(): Array<string> {}
function greet(): Array<Array<string>> {}
function greet(param: Array<string>): string {}
function greet(param: Array<string>): Array<string> {}
```

## 使用一致的类型声明

```js
// 错误
// use lower-case primitives for consistency
const str: String = "foo";
const bool: Boolean = true;
const num: Number = 1;
const symb: Symbol = Symbol("foo");

// use a proper function type
const func: Function = () => 1;

// use safer object types
const lowerObj: object = {};

const capitalObj1: Object = 1;
const capitalObj2: Object = { a: "string" };

const curly1: {} = 1;
const curly2: {} = { a: "string" };
// 正确
// use lower-case primitives for consistency
const str: string = "foo";
const bool: boolean = true;
const num: number = 1;
const symb: symbol = Symbol("foo");

// use a proper function type
const func: () => number = () => 1;

// use safer object types
const lowerObj: Record<string, unknown> = {};

const capitalObj1: number = 1;
const capitalObj2: { a: string } = { a: "string" };

const curly1: number = 1;
const curly2: Record<"a", string> = { a: "string" };
```

## 接口和类名使用大驼峰

```js
// 错误
class invalidClassName {}
interface someInterface {}

// 正确
class ValidClassName {}
interface SomeInterface {}
```

## 成员参数统一分隔符

```js
// 错误
interface Foo {
  name: string;
  greet(): void;
}

type Bar = {
  name: string,
  greet(): void,
};

// 正确
interface Foo {
  name: string;
  greet(): void;
}

type Bar = {
  name: string,
  greet(): void,
};
```

## 自动推断的类型不用写

```js
// 错误
const a: bigint = 10n;
const a: bigint = -10n;
const a: bigint = BigInt(10);
const a: bigint = -BigInt(10);
const a: boolean = false;
const a: boolean = true;
const a: boolean = Boolean(null);
const a: boolean = !0;
const a: number = 10;
const a: number = +10;
const a: number = -10;
const a: number = Number("1");
const a: number = +Number("1");
const a: number = -Number("1");
const a: number = Infinity;
const a: number = +Infinity;
const a: number = -Infinity;
const a: number = NaN;
const a: number = +NaN;
const a: number = -NaN;
const a: null = null;
const a: RegExp = /a/;
const a: RegExp = RegExp("a");
const a: RegExp = new RegExp("a");
const a: string = "str";
const a: string = `str`;
const a: string = String(1);
const a: symbol = Symbol("a");
const a: undefined = undefined;
const a: undefined = void someValue;

class Foo {
  prop: number = 5;
}

function fn(a: number = 5, b: boolean = true) {}

// 正确
const a = 10n;
const a = -10n;
const a = BigInt(10);
const a = -BigInt(10);
const a = false;
const a = true;
const a = Boolean(null);
const a = !0;
const a = 10;
const a = +10;
const a = -10;
const a = Number("1");
const a = +Number("1");
const a = -Number("1");
const a = Infinity;
const a = +Infinity;
const a = -Infinity;
const a = NaN;
const a = +NaN;
const a = -NaN;
const a = null;
const a = /a/;
const a = RegExp("a");
const a = new RegExp("a");
const a = "str";
const a = `str`;
const a = String(1);
const a = Symbol("a");
const a = undefined;
const a = void someValue;

class Foo {
  prop = 5;
}

function fn(a = 5, b = true) {}

function fn(a: number, b: boolean, c: string) {}
```

## 模块声明使用规范

1. 用 ESModule 规范代替 namespace, 不使用`/// <reference path="foo" />` ;
2. 用`declare module [name]`声明外部类型；

```js
// 错误
// types.ts
namespace Types {
  interface Foo {}
  interface Bar {}
}

// code.ts
/// <reference path="./types" />
const foo: Types.Foo = {};
const bar: Types.Bar = {};

// 正确
// types.ts
export interface Foo {}
export interface Bar {}

// code.ts
import * as Types from "./types"

const foo: Types.Foo = {};
const bar: Types.Bar = {};

// 错误
// if outside a d.ts file
module foo {}
namespace foo {}

// if outside a d.ts file and allowDeclarations = false
module foo {}
namespace foo {}
declare module foo {}
declare namespace foo {}

// 正确
// inside a d.ts file
declare module 'foo' {}
```

## 使用联合类型代替重载语法

```js
// 错误
function f(x: number): void;
function f(x: string): void;
f(): void;
f(...x: number[]): void;

// 正确
function f(x: number | string): void;
function f(x?: ...number[]): void;
```

## 数组类型声明规范

```js
// 错误
const a: (string | number)[] = ['a', 'b'];
const b: { prop: string }[] = [{ prop: 'a' }];
const c: (() => void)[] = [() => {}];
const d: Array<MyType> = ['a', 'b'];
const e: Array<string> = ['a', 'b'];
const f: ReadonlyArray<string> = ['a', 'b'];

// 正确
const a: Array<string | number> = ['a', 'b'];
const b: Array<{ prop: string }> = [{ prop: 'a' }];
const c: Array<() => void> = [() => {}];
const d: MyType[] = ['a', 'b'];
const e: string[] = ['a', 'b'];
const f: readonly string[] = ['a', 'b'];
```
