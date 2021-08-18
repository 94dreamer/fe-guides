# JavaScript规范

## 规则示例

- **使用两个空格**进行缩进

  rule: [`indent`](http://eslint.org/docs/rules/indent)

  ```javascript
  function hello (name) {
    console.log('hi', name);
  }
  ```

- 除需要转义的情况外，**字符串统一使用单引号**

  rule: [`quotes`](http://eslint.org/docs/rules/quotes)

  ```javascript
  console.log('hello there');
  $("<div class='box'>");
  ```

- **使用分号**

  rule: [`semi`](http://eslint.org/docs/rules/semi)

  ```javascript
  window.alert('hi');   // ✓ GOOD
  window.alert('hi')    // ✗ BAD
  ```

- **不要定义未使用的变量**

  rule: [`no-unused-vars`](http://eslint.org/docs/rules/no-unused-vars)

  ```javascript
  function myFunction () {
    var result = something();   // ✗ BAD
  }
  ```

- **关键字后面加空格**

  rule: [`keyword-spacing`](http://eslint.org/docs/rules/keyword-spacing)

  ```javascript
  if (condition) { ... }   // ✓ GOOD
  if(condition) { ... }    // ✗ BAD
  ```

- **函数声明时括号与函数名间加空格**

  rule: [`space-before-function-paren`](http://eslint.org/docs/rules/space-before-function-paren)

  ```javascript
  function name (arg) { ... }   // ✓ GOOD
  function name(arg) { ... }    // ✗ BAD
  
  run(function () { ... });      // ✓ GOOD
  run(function() { ... });       // ✗ BAD
  ```

- **始终使用** `===` 替代 `==`
  例外： `obj == null` 可以用来检查 `null || undefined`

  rule: [`eqeqeq`](http://eslint.org/docs/rules/eqeqeq)

  ```javascript
  if (name === 'John')   // ✓ GOOD
  if (name == 'John')    // ✗ BAD
  ```

  ```javascript
  if (name !== 'John')   // ✓ GOOD
  if (name != 'John')    // ✗ BAD
  ```

- **字符串拼接操作符 (Infix operators)** 之间要留空格

  rule: [`space-infix-ops`](http://eslint.org/docs/rules/space-infix-ops)

  ```javascript
  // ✓ GOOD
  var x = 2;
  var message = 'hello, ' + name + '!';
  ```

  ```javascript
  // ✗ BAD
  var x=2;
  var message = 'hello, '+name+'!';
  ```

- **逗号后面加空格**

  rule: [`comma-spacing`](http://eslint.org/docs/rules/comma-spacing)

  ```javascript
  // ✓ GOOD
  var list = [1, 2, 3, 4];
  function greet (name, options) { ... }
  ```

  ```javascript
  // ✗ BAD
  var list = [1,2,3,4];
  function greet (name,options) { ... }
  ```

- **else 关键字要与花括号**保持在同一行

  rule: [`brace-style`](http://eslint.org/docs/rules/brace-style)

  ```javascript
  // ✓ GOOD
  if (condition) {
    // ...
  } else {
    // ...
  }
  ```

  ```javascript
  // ✗ BAD
  if (condition)
  {
    // ...
  }
  else
  {
    // ...
  }
  ```

- **多行 if 语句的**的括号不能省

  rule: [`curly`](http://eslint.org/docs/rules/curly)

  ```javascript
  // ✓ GOOD
  if (options.quiet !== true) console.log('done');
  ```

  ```javascript
  // ✓ GOOD
  if (options.quiet !== true) {
    console.log('done');
  }
  ```

  ```javascript
  // ✗ BAD
  if (options.quiet !== true)
    console.log('done');
  ```

- **不要丢掉**异常处理中`err`参数

  rule: [`handle-callback-err`](http://eslint.org/docs/rules/handle-callback-err)

  ```javascript
  // ✓ GOOD
  run(function (err) {
    if (err) throw err;
    window.alert('done');
  })
  ```

  ```javascript
  // ✗ BAD
  run(function (err) {
    window.alert('done');
  });
  ```

- **使用浏览器全局变量时加上** `window.` 前缀
  Exceptions are: `document`, `console` and `navigator`.

  rule: [`no-undef`](http://eslint.org/docs/rules/no-undef)

  ```javascript
  window.alert('hi');   // ✓ GOOD
  ```

- **不允许有连续多行空行**

  rule: [`no-multiple-empty-lines`](http://eslint.org/docs/rules/no-multiple-empty-lines)

  ```javascript
  // ✓ GOOD
  var person = {};
  person.name = 'nikki';
  
  // BAD
  var person = {};
  // 超过1行以上的空行
  person.name = 'nikki';
  ```

- **对于三元运算符**

  `?` 和 `:` 与他们所负责的代码处于同一行

  rule: [`operator-linebreak`](http://eslint.org/docs/rules/operator-linebreak)

  ```javascript
  // ✓ GOOD
  var location = env.development ? 'localhost' : 'www.api.com';
  
  // ✓ GOOD
  var location = env.development
    ? 'localhost'
    : 'www.api.com';
  
  // ✗ BAD
  var location = env.development ?
    'localhost' :
    'www.api.com';
  ```

- **每个 var 关键字**单独声明一个变量

  rule: [`one-var`](http://eslint.org/docs/rules/one-var)

  ```javascript
  // ✓ GOOD
  var silent = true;
  var verbose = true;
  
  // ✗ BAD
  var silent = true, verbose = true;
  
  // ✗ BAD
  var silent = true,
      verbose = true;
  ```

- **条件语句中赋值语句**使用括号包起来这样使得代码更加清晰可读，而不会认为是将条件判断语句的全等号（`===`）错写成了等号（`=`）

  rule: [`no-cond-assign`](http://eslint.org/docs/rules/no-cond-assign)

  ```javascript
  // ✓ GOOD
  while ((m = text.match(expr))) {
    // ...
  }
  
  // ✗ BAD
  while (m = text.match(expr)) {
    // ...
  }
  ```

- **单行代码块两边加空格**

  rule: [`block-spacing`](http://eslint.org/docs/rules/block-spacing)

  ```javascript
    function foo () {return true}    // ✗ BAD
    function foo () { return true }  // ✓ GOOD
  ```

- **对于变量和函数名统一使用驼峰命名法**

  rule: [`camelcase`](http://eslint.org/docs/rules/camelcase)

  ```javascript
    function my_function () { }    // ✗ BAD
    function myFunction () { }     // ✓ GOOD
  
    var my_var = 'hello';           // ✗ BAD
    var myVar = 'hello';            // ✓ GOOD
  ```

- **不允许有多余的行末逗号**

  rule: [`comma-dangle`](http://eslint.org/docs/rules/comma-dangle)

  ```javascript
    var obj = {
      message: 'hello',   // ✗ BAD
    };
  ```

- **始终将逗号置于行末**

  rule: [`comma-style`](http://eslint.org/docs/rules/comma-style)

  ```javascript
    var obj = {
      foo: 'foo'
      ,bar: 'bar'   // ✗ BAD
    };
  
    var obj = {
      foo: 'foo',
      bar: 'bar'   // ✓ GOOD
    };
  ```

- **点号操作符须与属性需在同一行**

  rule: [`dot-location`](http://eslint.org/docs/rules/dot-location)

  ```javascript
    console.
      log('hello');  // ✗ BAD
  
    console
      .log('hello'); // ✓ GOOD
  ```

- **文件末尾留一空行**

  rule: [`eol-last`](http://eslint.org/docs/rules/eol-last)

- **函数调用时标识符与括号间不留间隔**

  rule: [`func-call-spacing`](http://eslint.org/docs/rules/func-call-spacing)

  ```javascript
  console.log ('hello'); // ✗ BAD
  console.log('hello');  // ✓ GOOD
  ```

- **键值对当中冒号与值之间要留空白**

  rule: [`key-spacing`](http://eslint.org/docs/rules/key-spacing)

  ```javascript
  var obj = { 'key' : 'value' };    // ✗ BAD
  var obj = { 'key' :'value' };     // ✗ BAD
  var obj = { 'key':'value' };      // ✗ BAD
  var obj = { 'key': 'value' };     // ✓ GOOD
  ```

- **构造函数要以大写字母开头**

  rule: [`new-cap`](http://eslint.org/docs/rules/new-cap)

  ```javascript
  function animal () {}
  var dog = new animal();    // ✗ BAD
  
  function Animal () {}
  var dog = new Animal();    // ✓ GOOD
  ```

- **无参的构造函数调用时要带上括号**

  rule: [`new-parens`](http://eslint.org/docs/rules/new-parens)

  ```javascript
  function Animal () {}
  var dog = new Animal;    // ✗ BAD
  var dog = new Animal();  // ✓ GOOD
  ```

- **对象中定义了存值器，一定要对应的定义取值器**

  rule: [`accessor-pairs`](http://eslint.org/docs/rules/accessor-pairs)

  ```javascript
  var person = {
    set name (value) {    // ✗ BAD
      this._name = value;
    },
  };
  
  var person = {
    set name (value) {
      this._name = value;
    },
    get name () {         // ✓ GOOD
      return this._name;
    },
  };
  ```

- **子类的构造器中一定要调用 `super`**

  rule: [`constructor-super`](http://eslint.org/docs/rules/constructor-super)

  ```javascript
  class Dog {
    constructor () {
      super();   // ✗ BAD
    },
  }
  
  class Dog extends Mammal {
    constructor () {
      super();   // ✓ GOOD
    },
  }
  ```

- **使用数组字面量而不是构造器**

  rule: [`no-array-constructor`](http://eslint.org/docs/rules/no-array-constructor)

  ```javascript
  var nums = new Array(1, 2, 3);   // ✗ BAD
  var nums = [1, 2, 3];            // ✓ GOOD
  ```

- **避免使用 `arguments.callee` 和 `arguments.caller`**

  rule: [`no-caller`](http://eslint.org/docs/rules/no-caller)

  ```javascript
  function foo (n) {
    if (n <= 0) return;
  
    arguments.callee(n - 1);   // ✗ BAD
  }
  
  function foo (n) {
    if (n <= 0) return;
  
    foo(n - 1);
  }
  ```

- **避免对类名重新赋值**

  rule: [`no-class-assign`](http://eslint.org/docs/rules/no-class-assign)

  ```javascript
  class Dog {}
  Dog = 'Fido';    // ✗ BAD
  ```

- **避免修改使用 `const` 声明的变量**

  rule: [`no-const-assign`](http://eslint.org/docs/rules/no-const-assign)

  ```javascript
  const score = 100;
  score = 125;       // ✗ BAD
  ```

- **避免使用常量作为条件表达式的条件（循环语句除外）**

  rule: [`no-constant-condition`](http://eslint.org/docs/rules/no-constant-condition)

  ```javascript
  if (false) {    // ✗ BAD
    // ...
  }
  
  if (x === 0) {  // ✓ GOOD
    // ...
  }
  
  while (true) {  // ✓ GOOD
    // ...
  }
  ```

- **正则中不要使用控制符**

  rule: [`no-control-regex`](http://eslint.org/docs/rules/no-control-regex)

  ```javascript
  var pattern = /\x1f/;    // ✗ BAD
  var pattern = /\x20/;    // ✓ GOOD
  ```

- **不要使用 `debugger`**

  rule: [`no-debugger`](http://eslint.org/docs/rules/no-debugger)

  ```javascript
  function sum (a, b) {
    debugger;      // ✗ BAD
    return a + b;
  }
  ```

- **不要对变量使用 `delete` 操作**

  rule: [`no-delete-var`](http://eslint.org/docs/rules/no-delete-var)

  ```javascript
  var name;
  delete name;     // ✗ BAD
  ```

- **不要定义冗余的函数参数**

  rule: [`no-dupe-args`](http://eslint.org/docs/rules/no-dupe-args)

  ```javascript
  function sum (a, b, a) {  // ✗ BAD
    // ...
  }
  
  function sum (a, b, c) {  // ✓ GOOD
    // ...
  }
  ```

- **类中不要定义冗余的属性**

  rule: [`no-dupe-class-members`](http://eslint.org/docs/rules/no-dupe-class-members)

  ```javascript
  class Dog {
    bark () {},
    bark () {},    // ✗ BAD
  }
  ```

- **对象字面量中不要定义重复的属性**

  rule: [`no-dupe-keys`](http://eslint.org/docs/rules/no-dupe-keys)

  ```javascript
  var user = {
    name: 'Jane Doe',
    name: 'John Doe',    // ✗ BAD
  }
  ```

- **`switch` 语句中不要定义重复的 `case` 分支**

  rule: [`no-duplicate-case`](http://eslint.org/docs/rules/no-duplicate-case)

  ```javascript
  switch (id) {
    case 1:
      // ...
    case 1:     // ✗ BAD
  }
  ```

- **同一模块有多个导入时一次性写完**

  rule: [`no-duplicate-imports`](http://eslint.org/docs/rules/no-duplicate-imports)

  ```javascript
  import { myFunc1 } from 'module';
  import { myFunc2 } from 'module';          // ✗ BAD
  
  import { myFunc1, myFunc2 } from 'module'; // ✓ GOOD
  ```

- **正则中不要使用空字符**

  rule: [`no-empty-character-class`](http://eslint.org/docs/rules/no-empty-character-class)

  ```javascript
  const myRegex = /^abc[]/;      // ✗ BAD
  const myRegex = /^abc[a-z]/;   // ✓ GOOD
  ```

- **不要解构空值**

  rule: [`no-empty-pattern`](http://eslint.org/docs/rules/no-empty-pattern)

  ```javascript
  const { a: {} } = foo;         // ✗ BAD
  const { a: { b } } = foo;      // ✓ GOOD
  ```

- **不要使用 `eval()`**

  rule: [`no-eval`](http://eslint.org/docs/rules/no-eval)

  ```javascript
  eval( "var result = user." + propName ); // ✗ BAD
  var result = user[propName];             // ✓ GOOD
  ```

- **`catch` 中不要对错误重新赋值**

  rule: [`no-ex-assign`](http://eslint.org/docs/rules/no-ex-assign)

  ```javascript
  try {
    // ...
  } catch (e) {
    e = 'new value';             // ✗ BAD
  }
  
  try {
    // ...
  } catch (e) {
    const newVal = 'new value';  // ✓ GOOD
  }
  ```

- **不要扩展原生对象**

  rule: [`no-extend-native`](http://eslint.org/docs/rules/no-extend-native)

  ```javascript
  Object.prototype.age = 21;     // ✗ BAD
  ```

- **避免多余的函数上下文绑定**

  rule: [`no-extra-bind`](http://eslint.org/docs/rules/no-extra-bind)

  ```javascript
  const name = function () {
    getName();
  }.bind(user);    // ✗ BAD
  
  const name = function () {
    this.getName();
  }.bind(user);    // ✓ GOOD
  ```

- **避免不必要的布尔转换**

  rule: [`no-extra-boolean-cast`](http://eslint.org/docs/rules/no-extra-boolean-cast)

  ```javascript
  const result = true;
  if (!!result) {   // ✗ BAD
    // ...
  }
  
  const result = true;
  if (result) {     // ✓ GOOD
    // ...
  }
  ```

- **不要使用多余的括号包裹函数**

  rule: [`no-extra-parens`](http://eslint.org/docs/rules/no-extra-parens)

  ```javascript
  const myFunc = (function () { });   // ✗ BAD
  const myFunc = function () { };     // ✓ GOOD
  ```

- **`switch` 一定要使用 `break` 来将条件分支正常中断**

  rule: [`no-fallthrough`](http://eslint.org/docs/rules/no-fallthrough)

  ```javascript
  switch (filter) {
    case 1:
      doSomething();    // ✗ BAD
    case 2:
      doSomethingElse();
  }
  
  switch (filter) {
    case 1:
      doSomething();
      break           // ✓ GOOD
    case 2:
      doSomethingElse();
  }
  
  switch (filter) {
    case 1:
      doSomething();
      // fallthrough  // ✓ GOOD
    case 2:
      doSomethingElse();
  }
  ```

- **不要省去小数点前面的0**

  rule: [`no-floating-decimal`](http://eslint.org/docs/rules/no-floating-decimal)

  ```javascript
  const discount = .5;      // ✗ BAD
  const discount = 0.5;     // ✓ GOOD
  ```

- **避免对声明过的函数重新赋值**

  rule: [`no-func-assign`](http://eslint.org/docs/rules/no-func-assign)

  ```javascript
  function myFunc () { }
  myFunc = myOtherFunc;    // ✗ BAD
  ```

- **不要对全局只读对象重新赋值**

  rule: [`no-global-assign`](http://eslint.org/docs/rules/no-global-assign)

  ```javascript
  window = {};     // ✗ BAD
  ```

- **注意隐式的 `eval()`**

  rule: [`no-implied-eval`](http://eslint.org/docs/rules/no-implied-eval)

  ```javascript
  setTimeout("alert('Hello world')");                   // ✗ BAD
  setTimeout(function () { alert('Hello world') });     // ✓ GOOD
  ```

- **嵌套的代码块中禁止再定义函数**

  rule: [`no-inner-declarations`](http://eslint.org/docs/rules/no-inner-declarations)

  ```javascript
  if (authenticated) {
    function setAuthUser () {}    // ✗ BAD
  }
  ```

- **不要向 `RegExp` 构造器传入非法的正则表达式**

  rule: [`no-invalid-regexp`](http://eslint.org/docs/rules/no-invalid-regexp)

  ```javascript
  RegExp('[a-z');    // ✗ BAD
  RegExp('[a-z]');   // ✓ GOOD
  ```

- **不要使用非法的空白符**

  rule: [`no-irregular-whitespace`](http://eslint.org/docs/rules/no-irregular-whitespace)

  ```javascript
  function myFunc () /*<NBSP>*/{}   // ✗ BAD
  ```

- **禁止使用 `__iterator__`**

  rule: [`no-iterator`](http://eslint.org/docs/rules/no-iterator)

  ```javascript
  Foo.prototype.__iterator__ = function () {};   // ✗ BAD
  ```

- **外部变量不要与对象属性重名**

  rule: [`no-label-var`](http://eslint.org/docs/rules/no-label-var)

  ```javascript
  var score = 100;
  function game () {
    score: while (true) {      // ✗ BAD
      score -= 10;
      if (score > 0) continue score;
      break;
    }
  }
  ```

- **不要使用标签语句**

  rule: [`no-labels`](http://eslint.org/docs/rules/no-labels)

  ```javascript
  label:
    while (true) {
      break label;     // ✗ BAD
    }
  ```

- **不要书写不必要的嵌套代码块**

  rule: [`no-lone-blocks`](http://eslint.org/docs/rules/no-lone-blocks)

  ```javascript
  function myFunc () {
    {                   // ✗ BAD
      myOtherFunc();
    }
  }
  
  function myFunc () {
    myOtherFunc();       // ✓ GOOD
  }
  ```

- **不要混合使用空格与制表符作为缩进**

  rule: [`no-mixed-spaces-and-tabs`](http://eslint.org/docs/rules/no-mixed-spaces-and-tabs)

- **除了缩进，不要使用多个空格**

  rule: [`no-multi-spaces`](http://eslint.org/docs/rules/no-multi-spaces)

  ```javascript
  const id =    1234;    // ✗ BAD
  const id = 1234;       // ✓ GOOD
  ```

- **不要使用多行字符串**

  rule: [`no-multi-str`](http://eslint.org/docs/rules/no-multi-str)

  ```javascript
  const message = 'Hello \
                   world';     // ✗ BAD
  ```

- **`new` 创建对象实例后需要赋值给变量**

  rule: [`no-new`](http://eslint.org/docs/rules/no-new)

  ```javascript
  new Character();                     // ✗ BAD
  const character = new Character();   // ✓ GOOD
  ```

- **禁止使用 `Function` 构造器**

  rule: [`no-new-func`](http://eslint.org/docs/rules/no-new-func)

  ```javascript
  var sum = new Function('a', 'b', 'return a + b');    // ✗ BAD
  ```

- **禁止使用 `Object` 构造器**

  rule: [`no-new-object`](http://eslint.org/docs/rules/no-new-object)

  ```javascript
  let config = new Object();   // ✗ BAD
  ```

- **禁止使用 `new require`**

  rule: [`no-new-require`](http://eslint.org/docs/rules/no-new-require)

  ```javascript
  const myModule = new require('my-module');    // ✗ BAD
  ```

- **禁止使用 `Symbol` 构造器**

  rule: [`no-new-symbol`](http://eslint.org/docs/rules/no-new-symbol)

  ```javascript
  const foo = new Symbol('foo');   // ✗ BAD
  ```

- **禁止使用原始包装器**

  rule: [`no-new-wrappers`](http://eslint.org/docs/rules/no-new-wrappers)

  ```javascript
  const message = new String('hello');   // ✗ BAD
  ```

- **不要将全局对象的属性作为函数调用**

  rule: [`no-obj-calls`](http://eslint.org/docs/rules/no-obj-calls)

  ```javascript
  const math = Math();   // ✗ BAD
  ```

- **不要使用八进制字面量**

  rule: [`no-octal`](http://eslint.org/docs/rules/no-octal)

  ```javascript
  const num = 042;     // ✗ BAD
  const num = '042';   // ✓ GOOD
  ```

- **字符串字面量中也不要使用八进制转义字符**

  rule: [`no-octal-escape`](http://eslint.org/docs/rules/no-octal-escape)

  ```javascript
  const copyright = 'Copyright \251';  // ✗ BAD
  ```

- **使用 `__dirname` 和 `__filename` 时尽量避免使用字符串拼接**

  rule: [`no-path-concat`](http://eslint.org/docs/rules/no-path-concat)

  ```javascript
  const pathToFile = __dirname + '/app.js';            // ✗ BAD
  const pathToFile = path.join(__dirname, 'app.js');   // ✓ GOOD
  ```

- 使用 `getPrototypeOf` 来替代 **`__proto__`**

  rule: [`no-proto`](http://eslint.org/docs/rules/no-proto)

  ```javascript
  const foo = obj.__proto__;               // ✗ BAD
  const foo = Object.getPrototypeOf(obj);  // ✓ GOOD
  ```

- **不要重复声明变量**

  rule: [`no-redeclare`](http://eslint.org/docs/rules/no-redeclare)

  ```javascript
  let name = 'John';
  let name = 'Jane';     // ✗ BAD
  
  let name = 'John';
  name = 'Jane';         // ✓ GOOD
  ```

- **正则中避免使用多个空格**

  rule: [`no-regex-spaces`](http://eslint.org/docs/rules/no-regex-spaces)

  ```javascript
  const regexp = /test   value/;   // ✗ BAD
  
  const regexp = /test {3}value/;  // ✓ GOOD
  const regexp = /test value/;     // ✓ GOOD
  ```

- **return 语句中的赋值必需有括号包裹**

  rule: [`no-return-assign`](http://eslint.org/docs/rules/no-return-assign)

  ```javascript
  function sum (a, b) {
    return result = a + b;     // ✗ BAD
  }
  
  function sum (a, b) {
    return (result = a + b);   // ✓ GOOD
  }
  ```

- **避免将变量赋值给自己**

  rule: [`no-self-assign`](http://eslint.org/docs/rules/no-self-assign)

  ```javascript
  name = name;   // ✗ BAD
  ```

- **避免将变量与自己进行比较操作**

  esint: [`no-self-compare`](http://eslint.org/docs/rules/no-self-compare)

  ```javascript
  if (score === score) {}   // ✗ BAD
  ```

- **避免使用逗号操作符**

  rule: [`no-sequences`](http://eslint.org/docs/rules/no-sequences)

  ```javascript
  if (doSomething(), !!test) {}   // ✗ BAD
  ```

- **不要随意更改关键字的值**

  rule: [`no-shadow-restricted-names`](http://eslint.org/docs/rules/no-shadow-restricted-names)

  ```javascript
  let undefined = 'value';     // ✗ BAD
  ```

- **禁止使用稀疏数组（Sparse arrays）**

  rule: [`no-sparse-arrays`](http://eslint.org/docs/rules/no-sparse-arrays)

  ```javascript
  let fruits = ['apple',, 'orange'];       // ✗ BAD
  ```

- **不要使用制表符**

  rule: [`no-tabs`](http://eslint.org/docs/rules/no-tabs)

- **正确使用 ES6 中的字符串模板**

  rule: [`no-template-curly-in-string`](http://eslint.org/docs/rules/no-template-curly-in-string)

  ```javascript
  const message = 'Hello ${name}';   // ✗ BAD
  const message = `Hello ${name}`;   // ✓ GOOD
  ```

- **使用 `this` 前请确保 `super()` 已调用**

  rule: [`no-this-before-super`](http://eslint.org/docs/rules/no-this-before-super)

  ```javascript
  class Dog extends Animal {
    constructor () {
      this.legs = 4;     // ✗ BAD
      super();
    }
  }
  ```

- **用 `throw` 抛错时，抛出 `Error` 对象而不是字符串**

  rule: [`no-throw-literal`](http://eslint.org/docs/rules/no-throw-literal)

  ```javascript
  throw 'error';               // ✗ BAD
  throw new Error('error');    // ✓ GOOD
  ```

- **行末不留空格**

  rule: [`no-trailing-spaces`](http://eslint.org/docs/rules/no-trailing-spaces)

- **不要使用 `undefined` 来初始化变量**

  rule: [`no-undef-init`](http://eslint.org/docs/rules/no-undef-init)

  ```javascript
  let name = undefined;    // ✗ BAD
  
  let name
  name = 'value';          // ✓ GOOD
  ```

- **循环语句中注意更新循环变量**

  rule: [`no-unmodified-loop-condition`](http://eslint.org/docs/rules/no-unmodified-loop-condition)

  ```javascript
  for (let i = 0; i < items.length; j++) {...}    // ✗ BAD
  for (let i = 0; i < items.length; i++) {...}    // ✓ GOOD
  ```

- **如果有更好的实现，尽量不要使用三元表达式**

  rule: [`no-unneeded-ternary`](http://eslint.org/docs/rules/no-unneeded-ternary)

  ```javascript
  let score = val ? val : 0;     // ✗ BAD
  let score = val || 0;          // ✓ GOOD
  ```

- **`return`，`throw`，`continue` 和 `break` 后不要再跟代码**

  rule: [`no-unreachable`](http://eslint.org/docs/rules/no-unreachable)

  ```javascript
  function doSomething () {
    return true;
    console.log('never called');     // ✗ BAD
  }
  ```

- **`finally` 代码块中不要再改变程序执行流程**

  rule: [`no-unsafe-finally`](http://eslint.org/docs/rules/no-unsafe-finally)

  ```javascript
  try {
    // ...
  } catch (e) {
    // ...
  } finally {
    return 42;     // ✗ BAD
  }
  ```

- **关系运算符的左值不要做取反操作**

  rule: [`no-unsafe-negation`](http://eslint.org/docs/rules/no-unsafe-negation)

  ```javascript
  if (!key in obj) {}       // ✗ BAD
  ```

- **避免不必要的 `.call()` 和 `.apply()`**

  rule: [`no-useless-call`](http://eslint.org/docs/rules/no-useless-call)

  ```javascript
  sum.call(null, 1, 2, 3);   // ✗ BAD
  ```

- **避免使用不必要的计算值作对象属性**

  rule: [`no-useless-computed-key`](http://eslint.org/docs/rules/no-useless-computed-key)

  ```javascript
  const user = { ['name']: 'John Doe' };   // ✗ BAD
  const user = { name: 'John Doe' };       // ✓ GOOD
  ```

- **禁止多余的构造器**

  rule: [`no-useless-constructor`](http://eslint.org/docs/rules/no-useless-constructor)

  ```javascript
  class Car {
    constructor () {      // ✗ BAD
    }
  }
  ```

- **禁止不必要的转义**

  rule: [`no-useless-escape`](http://eslint.org/docs/rules/no-useless-escape)

  ```javascript
  let message = 'Hell\o';  // ✗ BAD
  ```

- **import, export 和解构操作中，禁止赋值到同名变量**

  rule: [`no-useless-rename`](http://eslint.org/docs/rules/no-useless-rename)

  ```javascript
  import { config as config } from './config';     // ✗ BAD
  import { config } from './config';               // ✓ GOOD
  ```

- **属性前面不要加空格**

  rule: [`no-whitespace-before-property`](http://eslint.org/docs/rules/no-whitespace-before-property)

  ```javascript
  user .name      // ✗ BAD
  user.name       // ✓ GOOD
  ```

- **禁止使用 `with`**

  rule: [`no-with`](http://eslint.org/docs/rules/no-with)

  ```javascript
  with (val) {...}    // ✗ BAD
  ```

- **对象属性换行时注意统一代码风格**

  rule: [`object-property-newline`](http://eslint.org/docs/rules/object-property-newline)

  ```javascript
  const user = {
    name: 'Jane Doe', age: 30,
    username: 'jdoe86',            // ✗ BAD
  };
  
  const user = { name: 'Jane Doe', age: 30, username: 'jdoe86' };    // ✓ GOOD
  
  const user = {
    name: 'Jane Doe',
    age: 30,
    username: 'jdoe86',
  };                                                                 // ✓ GOOD
  ```

- **代码块中避免多余留白**

  rule: [`padded-blocks`](http://eslint.org/docs/rules/padded-blocks)

  ```javascript
  if (user) {
                              // ✗ BAD
    const name = getName();
  
  }
  
  if (user) {
    const name = getName();    // ✓ GOOD
  }
  ```

- **展开运算符与它的表达式间不要留空白**

  rule: [`rest-spread-spacing`](http://eslint.org/docs/rules/rest-spread-spacing)

  ```javascript
  fn(... args);    // ✗ BAD
  fn(...args);     // ✓ GOOD
  ```

- **遇到分号时空格要后留前不留**

  rule: [`semi-spacing`](http://eslint.org/docs/rules/semi-spacing)

  ```javascript
  for (let i = 0 ;i < items.length ;i++) {...}    // ✗ BAD
  for (let i = 0; i < items.length; i++) {...}    // ✓ GOOD
  ```

- **代码块首尾留空格**

  rule: [`space-before-blocks`](http://eslint.org/docs/rules/space-before-blocks)

  ```javascript
  if (admin){...}     // ✗ BAD
  if (admin) {...}    // ✓ GOOD
  ```

- **圆括号间不留空格**

  rule: [`space-in-parens`](http://eslint.org/docs/rules/space-in-parens)

  ```javascript
  getName( name );     // ✗ BAD
  getName(name);       // ✓ GOOD
  ```

- **一元运算符后面跟一个空格**

  rule: [`space-unary-ops`](http://eslint.org/docs/rules/space-unary-ops)

  ```javascript
  typeof!admin        // ✗ BAD
  typeof !admin        // ✓ GOOD
  ```

- **注释首尾留空格**

  rule: [`spaced-comment`](http://eslint.org/docs/rules/spaced-comment)

  ```javascript
  //comment           // ✗ BAD
  // comment          // ✓ GOOD
  
  /*comment*/         // ✗ BAD
  /* comment */       // ✓ GOOD
  ```

- **模板字符串中变量前后不加空格**

  rule: [`template-curly-spacing`](http://eslint.org/docs/rules/template-curly-spacing)

  ```javascript
  const message = `Hello, ${ name }`;    // ✗ BAD
  const message = `Hello, ${name}`;      // ✓ GOOD
  ```

- **检查 `NaN` 的正确姿势是使用 `isNaN()`**

  rule: [`use-isnan`](http://eslint.org/docs/rules/use-isnan)

  ```javascript
  if (price === NaN) { }      // ✗ BAD
  if (isNaN(price)) { }       // ✓ GOOD
  ```

- **用合法的字符串跟 `typeof` 进行比较操作**

  rule: [`valid-typeof`](http://eslint.org/docs/rules/valid-typeof)

  ```javascript
  typeof name === 'undefimed'     // ✗ BAD
  typeof name === 'undefined'     // ✓ GOOD
  ```

- **自调用匿名函数 (IIFEs) 使用括号包裹**

  rule: [`wrap-iife`](http://eslint.org/docs/rules/wrap-iife)

  ```javascript
  const getName = function () { }();     // ✗ BAD
  
  const getName = (function () { }());   // ✓ GOOD
  const getName = (function () { })();   // ✓ GOOD
  ```

- **`yield \*` 中的 `\*` 前后都要有空格**

  rule: [`yield-star-spacing`](http://eslint.org/docs/rules/yield-star-spacing)

  ```javascript
  yield* increment()    // ✗ BAD
  yield * increment()   // ✓ GOOD
  ```

- **请书写优雅的条件语句（avoid Yoda conditions）**

  rule: [`yoda`](http://eslint.org/docs/rules/yoda)

  ```javascript
  if (42 === age) { }    // ✗ BAD
  if (age === 42) { }    // ✓ GOOD
  ```

