## 一、规则示例

- **React 组件定义 displayName**

  rule: [`react/display-name`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/display-name.md)

  ```jsx
  // ✓ GOOD
  var Hello = createReactClass({
    displayName: 'Hello',
    render: function() {
      return <div>Hello {this.props.name}</div>;
    }
  });

  export default function Hello({ name }) {
    return <div>Hello {name}</div>;
  }
  Hello.displayName = 'Hello';

  // ✗ BAD
  var Hello = createReactClass({
    render: function() {
      return <div>Hello {this.props.name}</div>;
    }
  });

  export default function Hello({ name }) {
    return <div>Hello {name}</div>;
  }
  ```

- **检查缺少 key 属性的情况**

  rule: [`react/jsx-key`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-key.md)

  ```jsx
  // ✓ GOOD
  [<Hello key="first" />, <Hello key="second" />, <Hello key="third" />];

  data.map((x, i) => <Hello key={i}>{x}</Hello>);

  (<Hello key={id} {...{ id, caption }} />)[
    // ✗ BAD
    ((<Hello />), (<Hello />), (<Hello />))
  ];

  data.map((x) => <Hello>{x}</Hello>);

  <Hello {...{ key: id, id, caption }} />;
  ```

- **防止将注释作为文本节点插入**

  rule: [`react/jsx-no-comment-textnodes`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-no-comment-textnodes.md)

  ```jsx
  // ✓ GOOD
  var Hello = createReactClass({
    displayName: 'Hello',
    render: function() {
      return <div>{/* empty div */}</div>;
    }
  });

  var Hello = createReactClass({
    displayName: 'Hello',
    render: function() {
      return <div /* empty div */></div>;
    }
  });

  var Hello = createReactClass({
    displayName: 'Hello',
    render: function() {
      return <div className={'foo' /* temp class */}</div>;
    }
  });

  // ✗ BAD
  var Hello = createReactClass({
    render: function() {
      return (
        <div>// empty div</div>
      );
    }
  });

  var Hello = createReactClass({
    render: function() {
      return (
        <div>
          /* empty div */
        </div>
      );
    }
  });
  ```

- **防止 JSX 中的重复属性**

  rule: [`react/jsx-no-duplicate-props`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-no-duplicate-props.md)

  ```jsx
  // ✓ GOOD
  <Hello firstname="John" lastname="Doe" />;

  // ✗ BAD
  <Hello name="John" name="John" />;
  ```

- **防止使用不安全的`target='_blank'`**

  rule: [`react/jsx-no-target-blank`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-no-target-blank.md)

  ```jsx
  // ✓ GOOD
  var Hello = <p target="_blank"></p>;
  var Hello = (
    <a target="_blank" rel="noopener noreferrer" href="http://example.com"></a>
  );
  var Hello = <a target="_blank" href="relative/path/in/the/host"></a>;
  var Hello = <a target="_blank" href="/absolute/path/in/the/host"></a>;
  var Hello = <a></a>;

  // ✗ BAD
  var Hello = <a target="_blank" href="http://example.com/"></a>;
  var Hello = <a target="_blank" href={dynamicLink}></a>;
  ```

- **在 JSX 中先声明再使用**

  rule: [`react/jsx-no-undef`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-no-undef.md)

  ```jsx
  // ✓ GOOD
  var Hello = require("./Hello");

  <Hello name="John" />;

  // ✗ BAD
  <Hello name="John" />;
  ```

- **防止 React 被错误地标记为未使用**

  rule: [`react/jsx-uses-react`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-uses-react.md)

  ```jsx
  // ✓ GOOD
  var React = require("react");

  var Hello = <div>Hello {this.props.name}</div>;

  // ✗ BAD
  var React = require("react");

  // nothing to do with React
  ```

- **防止 JSX 中使用的变量被错误地标记为未使用**

  rule: [`react/jsx-uses-vars`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-uses-vars.md)

  ```jsx
  // ✓ GOOD
  var Hello = require("./Hello");

  <Hello name="John" />;

  // ✗ BAD
  var Hello = require("./Hello");
  ```

- **`children`不能被当做`props`**

  rule: [`react/no-children-prop`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-children-prop.md)

  ```jsx
  // ✓ GOOD
  <div>Children</div>

  <MyComponent>Children</MyComponent>

  <MyComponent>
    <span>Child 1</span>
    <span>Child 2</span>
  </MyComponent>

  React.createElement("div", {}, 'Children')
  React.createElement("div", 'Child 1', 'Child 2')

  // ✗ BAD
  <div children='Children' />

  <MyComponent children={<AnotherComponent />} />
  <MyComponent children={['Child 1', 'Child 2']} />

  React.createElement("div", { children: 'Children' })
  ```

- **`dangerouslySetInnerHTML`和`children`不能混用**

  rule: [`react/no-danger-with-children`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-danger-with-children.md)

- **不使用废弃的方法**

  rule: [`react/no-deprecated`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-deprecated.md)

  ```jsx
  // ✓ GOOD
  ReactDOM.render(<MyComponent />, root);

  // When [1, {"react": "0.13.0"}]
  ReactDOM.findDOMNode(this.refs.foo);

  import { PropTypes } from "prop-types";

  // ✗ BAD
  React.render(<MyComponent />, root);

  React.unmountComponentAtNode(root);

  React.findDOMNode(this.refs.foo);

  React.renderToString(<MyComponent />);

  React.renderToStaticMarkup(<MyComponent />);

  React.createClass({
    /* Class object */
  });

  const propTypes = {
    foo: PropTypes.bar,
  };

  //Any factories under React.DOM
  React.DOM.div();

  import React, { PropTypes } from "react";
  ```

- **禁止把`state`当做可变数据**

  rule: [`react/no-direct-mutation-state`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-direct-mutation-state.md)

  ```jsx
  // ✓ GOOD
  var Hello = createReactClass({
    componentDidMount: function() {
      this.setState({
        name: this.props.name.toUpperCase();
      });
    },
    render: function() {
      return <div>Hello {this.state.name}</div>;
    }
  });

  class Hello extends React.Component {
    constructor(props) {
      super(props)

      this.state = {
        foo: 'bar',
      }
    }
  }

  // ✗ BAD
  var Hello = createReactClass({
    componentDidMount: function() {
      this.state.name = this.props.name.toUpperCase();
    },
    render: function() {
      return <div>Hello {this.state.name}</div>;
    }
  });

  class Hello extends React.Component {
    constructor(props) {
      super(props)

      // Assign at instance creation time, not on a callback
      doSomethingAsync(() => {
        this.state = 'bad';
      });
    }
  }
  ```

- **禁止使用`findDOMNode`**

  rule: [`react/no-find-dom-node`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-find-dom-node.md)

  ```jsx
  // ✓ GOOD
  class MyComponent extends Component {
    componentDidMount() {
      this.node.scrollIntoView();
    }
    render() {
      return <div ref={(node) => (this.node = node)} />;
    }
  }

  // ✗ BAD
  class MyComponent extends Component {
    componentDidMount() {
      findDOMNode(this).scrollIntoView();
    }
    render() {
      return <div />;
    }
  }
  ```

- **禁止使用`isMounted`**

  rule: [`react/no-is-mounted`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-is-mounted.md)

  ```jsx
  // ✓ GOOD
  var Hello = createReactClass({
    render: function () {
      return <div onClick={this.props.handleClick}>Hello</div>;
    },
  });

  // ✗ BAD
  var Hello = createReactClass({
    handleClick: function () {
      setTimeout(function () {
        if (this.isMounted()) {
          return;
        }
      });
    },
    render: function () {
      return <div onClick={this.handleClick.bind(this)}>Hello</div>;
    },
  });
  ```

- **禁止使用`React.render`的返回值**

  rule: [`react/no-render-return-value`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-render-return-value.md)

  ```jsx
  // ✓ GOOD
  var Hello = createReactClass({
    displayName: "Hello",
    render: function () {
      return <div>Hello {this.props.name}</div>;
    },
  });

  // ✗ BAD
  var Hello = createReactClass({
    render: function () {
      return <div>Hello {this.props.name}</div>;
    },
  });
  ```

- **不使用字符串引用**

  rule: [`react/no-string-refs`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-string-refs.md)

  ```jsx
  // ✓ GOOD
  ReactDOM.render(<App ref={doSomethingWithInst} />, document.body);

  ReactDOM.render(<App />, document.body, doSomethingWithInst);

  // ✗ BAD
  const inst = ReactDOM.render(<App />, document.body);
  doSomethingWithInst(inst);
  ```

- **防止无效的标记**

  rule: [`react/no-unescaped-entities`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-unescaped-entities.md)

  ```jsx
  // ✗ BAD
  <MyComponent
    name="name"
    type="string"
    foo="bar">  {/* oops! */}
    x="y">
    Body Text
  </MyComponent>

  <MyComponent
    a="b">  {/* oops! */}
    c="d"
    Intended body text
  </MyComponent>

  <MyComponent>{'Text'}}</MyComponent>
  ```

- **不使用无效的属性**

  rule: [`react/no-unknown-property`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-unknown-property.md)

  ```jsx
  // ✓ GOOD
  var React = require("react");

  var Hello = <div className="hello">Hello World</div>;

  // ✗ BAD
  var React = require("react");

  var Hello = <div class="hello">Hello World</div>;
  ```

- **保证在`jsx`文件中有引入`React`**

  rule: [`react/react-in-jsx-scope`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/react-in-jsx-scope.md)

- **在`render`方法中必须有`return`**

  rule: [`react/require-render-return`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/require-render-return.md)

  ```jsx
  // ✓ GOOD
  var Hello = createReactClass({
    render() {
      return <div>Hello</div>;
    },
  });

  class Hello extends React.Component {
    render() {
      return <div>Hello</div>;
    }
  }

  // ✗ BAD
  var Hello = createReactClass({
    render() {
      <div>Hello</div>;
    },
  });

  class Hello extends React.Component {
    render() {
      <div>Hello</div>;
    }
  }
  ```

- **不要在循环、条件或者嵌套函数中调用`hooks`**

  rule: [`react-hooks/rules-of-hooks`](https://reactjs.org/docs/hooks-rules.html#only-call-hooks-at-the-top-level)

  **只在最顶层使用 Hook**

  不要在循环，条件或嵌套函数中调用 Hook， 确保总是在你的 React 函数的最顶层调用他们。遵守这条规则，你就能确保 Hook 在每一次渲染中都按照同样的顺序被调用。这让 React 能够在多次的 useState 和 useEffect 调用之间保持 hook 状态的正确。(如果你对此感到好奇，我们在下面会有更深入的解释。)

- **只在`React Function`中使用`hooks`**

  rule: [`react-hooks/exhaustive-deps`](https://reactjs.org/docs/hooks-rules.html#only-call-hooks-from-react-functions)

  **只在 React 函数中调用 Hook**

  不要在普通的 JavaScript 函数中调用 Hook。你可以：

  - ✅ 在 React 的函数组件中调用 Hook
  - ✅ 在自定义 Hook 中调用其他 Hook

  遵循此规则，确保组件的状态逻辑在代码中清晰可见。

## 二、后置阅读

更合理的方式书写 React 和 JSX，借鉴 Airbnb React 编码规范：[style-guide](https://github.com/minwe/style-guide)

[代码规范 - React]

## 基本规范

- **单文件不能超过 500 行**

- 每个文件只包含一个 React 组件
  - 无状态或者 pure 组件允许一个文件包含多个组件。
- 始终使用 JSX 语法
- 每个文件第一行为该文件的简略说明

## 组件创建方式

- 如果组件内部未使用状态或生命周期方法，优先使用普通函数创建组件：

## 命名规范

写别人看得懂的单词，全部用英语，不要出现汉语拼音或者首字母等，推荐使用谷歌翻译，尽量使用语义化的命名组合；

命名不要机翻，尽量精简短小而又不失其本意

- **扩展名**：使用 `.jsx` 作为 React 组件的扩展名；
- **文件夹名**：文件夹使用 snake_case 命名法;
- **文件名**：使用大驼峰命名法（PascalCase），如 `MyComponent.jsx`；
- **组件命名**：组件名称和文件名一致，如 `MyComponent.jsx` 里的组件名应该是 m`y-component`；一个目录的根组件使用 `index.jsx` 命名，以目录名称作为组件名称；
- **引用命名**：React 组件使用大驼峰命名法（PascalCase），组件实例使用小驼峰命名法（camelCase）；
- **变量**：小驼峰命名
- **常量**：全大些，用下划线分割单词
- 变量命名应该以名字作为前缀，而函数名前缀应当是动词（构造函数的命名通常是名词）

尽量在变量名中体现出值的数据类型。比如，命名`count`、`length`和`size`表明数据类型是数字，而命名`name`、`title`和`message`表明数据类型是字符串，过去分词表是布尔类型。

但用单个字符命名的变量诸如`i`、`j`和`k`通常在循环中使用。使用这些能够体现出数据类型的命名，可以让你的代码容易被别人和自己读懂。

要避免使用没有意义的命名，如：`foo`、`bar`和`tmp`。对于函数和方法命名来说，第一个单词应该是动词，这里有一些使用动词常见的约定：

| 动词 |         含义         |
| :--: | :------------------: |
| can  |  函数返回一个布尔值  |
| has  |  函数返回一个布尔值  |
|  is  |  函数返回一个布尔值  |
| get  | 函数返回一个非布尔值 |
| set  |  函数用来保存一个值  |

## 缩进

一般缩进为 2 个 space；

当一行长度达到了单行最大字符限制时，就需要手动将一行拆成两行。通常我们会在运算符后换行，下一行会增加两个层次的缩进；

## 空行

在下面这些场景中添加空行：

- 在方法之间。
- 在方法中的局部变量和第一条语句之间。
- 在多行或单行注释之前。
- 在方法内的逻辑片段之间插入空行，提高可读性。

## 注释

恰到好处的注释，**每个文件第一行都需要对该文件的作用简要说明**

- 不能太多或太少，注释的形式根据代码具体的情况有不同；
- 避免用注释包裹代码；
- 尽量留下简明扼要的注释；

### 单行注释

在双斜线后敲入一个空格，用来让注释文本有一定的偏移。

单行注释有三种使用方法：

- 独占一行的注释，用来解释下一行代码。这行注释之前总是有一个空行，且缩进层级和下一行代码保持一致。
- 在代码行的尾部的注释。代码结束到注释之间至少有一个缩进。注释（包括之前的代码部分）不应当超过最大字符数限制，如果超过了，就将这条注释放置于当前代码行的上方。
- 被注释的大段代码。

单行注释不应当以连续多行注释的形式出现，除非你注释掉一大段代码。只有当需要注释一段很长的文本时才使用多行注释。

### 多行注释

虽然多行注释也可以用于注释单行，但还是推荐仅在需要使用多行注释的时候，才使用多行注释。多行注释一般用于以下场景：

- 模块、类、函数开头的注释
- 需要使用多行注释

推荐使用 JsDoc 的注释风格。

## 括号

- 用括号包裹多行 JSX 标签;
- 单行 JSX 省略 `();```

## 花括号

左花括号放置在块语句中第一句代码的末尾

## 引号

- JSX 的属性都采用双引号，其他的 JS 都使用单引号

## 空格

- 终始在自闭合标签前面添加一个空格 <Foo />;

## 标签

- 当标签没有子元素时，始终时候自闭合标签;
- 属性较少时可以行内排列;
- 如果控件有多行属性，闭合标签单独成行;

## 属性

- React 组件的属性使用**小驼峰命名法**；
- 当属性值等于 true 的时候，省略该属性的赋值；
- 传递给 HTML 元素的自定义属性，需要添加 `data-` 前缀，React 不会渲染非标准属性；
- 属性较多使用 `{...this.props}` 语法；
- 属性 `=` 前后不要添加空格；
- JSX 中的花括号前后不要添加空格;
- 用 [Class Field](https://tc39.github.io/proposal-class-public-fields/) 定义类的成员变量，如 state，props，轻易不要使用 constructor;

## `propTypes` 及默认值

- 组件属性都应该在 `propTypes` 中声明类型；
- 始终明确指定非必选属性的默认值。

## 相等

- 做相等比较请用 `=== `和 !==，禁止使用 == 和 !=`。`
- `避免“空比较”：不要直接用 null/undefined 等判断`
  - `检测原始值：typeof value = 'string/number/boolean/null/undefined'`
  - `检测引用值：value instanceof constructor`
  - `检测函数：typeof Function === ‘function’`
  - `检测数组：Array.isArray()`
  - 检测属性：prop in object

## key

- 避免使用数组的索引作为 `key` 值，优先使用唯一 ID 作为 key 值
- 同时满足以下条件时可以使用数组索引作为 `key` 值：
  - 数组是静态的：不经过计算，也不会改变；
  - 数组项没有 id 或 alias 等唯一值;
  - 数组不做排序或者过滤操作。

## 方法

- 在 render 方法中事件的回调函数全部使用箭头函数遮蔽本地变量;
- React 组件的内部方法命名不要使用下划线前缀;
- `render` 方法中应该始终返回值;
- 直接返回 JSX 结构的方法以 render 开头，如 renderFooter();
- 事件处理方法以 `on` 开头，如 `onClick() {};`

## 条件判断

- 使用 && 替换不要的三元判断
- 使用 map 替换多分支判断

## Ref

- 始终使用 ref 回调 <Foo ref={ref => { this.myRef = ref; }} />

## 排序

- class extends React.Component 的顺序：
  - static propTypes = {}
  - static defaultProps = {}
  - state = {}
  - constructor // 最好不用
  - static getDerivedStateFromProps (nextProps, prevState)
  - componentDidMount ()
  - shouldComponentUpdate (nextProps, nextState)
  - getSnapshotBeforeUpdate (prevProps, prevState)
  - componentDidUpdate (prevProps, prevState)
  - componentWillUnmount ()
  - 事件处理方法
  - 其他操作方法
  - 请求方法
  - 包含 JSX 的方法，如 getColumns ()
  - render ()

componentWillMount、componentWillReceiveProps、componentWillUpdate 已被废弃，不要再使用

## for 循环

- 使用 for-in 循环遍历对象属性，使用 hasOwnProperty() 方法来为 for-in 循环过滤出实例属性；
- 使用 for-of 循环遍历数组；

## 请求

ajax 请求在 componentDidMount 生命周期发起。

## eval

禁止使用 eval

来源 [Airbnb React Style Guild](https://github.com/JasonBoy/javascript/blob/master/react/README.md)

## [Basic Rules 基本规范]

- 每个文件只写一个模块.
  - 但是多个[无状态模块](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions)可以放在单个文件中. eslint: [`react/no-multi-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-multi-comp.md#ignorestateless).
- 推荐使用 JSX 语法.
- 不要使用 `React.createElement`，除非从一个非 JSX 的文件中初始化你的 app.

## [创建模块]

Class vs React.createClass vs stateless

- 如果你的模块有内部状态或者是`refs`, 推荐使用 `class extends React.Component` 而不是 `React.createClass`. eslint: [`react/prefer-es6-class`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-es6-class.md) [`react/prefer-stateless-function`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-stateless-function.md)

  ```jsx
  // bad
  const Listing = React.createClass({
    // ...
    render() {
      return <div>{this.state.hello}</div>;
    },
  });

  // good
  class Listing extends React.Component {
    // ...
    render() {
      return <div>{this.state.hello}</div>;
    }
  }
  ```

  如果你的模块没有状态或是没有引用`refs`， 推荐使用普通函数（非箭头函数）而不是类:

  ```jsx
  // bad
  class Listing extends React.Component {
    render() {
      return <div>{this.props.hello}</div>;
    }
  }

  // bad (relying on function name inference is discouraged)
  const Listing = ({ hello }) => <div>{hello}</div>;

  // good
  function Listing({ hello }) {
    return <div>{hello}</div>;
  }
  ```

## [Mixins]

- [不要使用 mixins](https://facebook.github.io/react/blog/2016/07/13/mixins-considered-harmful.html).

  > 为什么? Mixins 会增加隐式的依赖，导致命名冲突，并且会以雪球式增加复杂度。在大多数情况下 Mixins 可以被更好的方法替代，如：组件化，高阶组件，工具模块等。

## [Naming 命名]

- **扩展名**: React 模块使用 `.jsx` 扩展名.

- **文件名**: 文件名使用帕斯卡命名. 如, `ReservationCard.jsx`.

- **引用命名**: React 模块名使用帕斯卡命名，实例使用骆驼式命名. eslint: [`react/jsx-pascal-case`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)

  ```jsx
  // bad
  import reservationCard from "./ReservationCard";

  // good
  import ReservationCard from "./ReservationCard";

  // bad
  const ReservationItem = <ReservationCard />;

  // good
  const reservationItem = <ReservationCard />;
  ```

- **模块命名**: 模块使用当前文件名一样的名称. 比如 `ReservationCard.jsx` 应该包含名为 `ReservationCard`的模块. 但是，如果整个文件夹是一个模块，使用 `index.js`作为入口文件，然后直接使用 `index.js` 或者文件夹名作为模块的名称:

  ```jsx
  // bad
  import Footer from "./Footer/Footer";

  // bad
  import Footer from "./Footer/index";

  // good
  import Footer from "./Footer";
  ```

- **高阶模块命名**: 对于生成一个新的模块，其中的模块名 `displayName` 应该为高阶模块名和传入模块名的组合. 例如, 高阶模块 `withFoo()`, 当传入一个 `Bar` 模块的时候， 生成的模块名 `displayName` 应该为 `withFoo(Bar)`.

  > 为什么？一个模块的 `displayName` 可能会在开发者工具或者错误信息中使用到，因此有一个能清楚的表达这层关系的值能帮助我们更好的理解模块发生了什么，更好的 Debug.

  ```jsx
  // bad
  export default function withFoo(WrappedComponent) {
    return function WithFoo(props) {
      return <WrappedComponent {...props} foo />;
    }
  }

  // good
  export default function withFoo(WrappedComponent) {
    function WithFoo(props) {
      return <WrappedComponent {...props} foo />;
    }

    const wrappedComponentName = WrappedComponent.displayName
      || WrappedComponent.name
      || 'Component';

    WithFoo.displayName = `withFoo(${wrappedComponentName})`;
    return WithFoo;
  }
  ```

- **属性命名**: 避免使用 DOM 相关的属性来用作其他的用途。

  > 为什么？对于`style` 和 `className`这样的属性名，我们都会默认它们代表一些特殊的含义，如元素的样式，CSS class 的名称。在你的应用中使用这些属性来表示其他的含义会使你的代码更难阅读，更难维护，并且可能会引起 bug。

  ```jsx
  // bad
  <MyComponent style="fancy" />

  // good
  <MyComponent variant="fancy" />
  ```

## [Declaration 声明模块]

- 不要使用 `displayName` 来命名 React 模块，而是使用引用来命名模块， 如 class 名称.

  ```jsx
  // bad
  export default React.createClass({
    displayName: 'ReservationCard',
    // stuff goes here
  });

  // good
  export default class ReservationCard extends React.Component {
  }
  ```

## [Alignment 代码对齐]

- 遵循以下的 JSX 语法缩进/格式. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md) [`react/jsx-closing-tag-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-tag-location.md)

  ```jsx
  // bad
  <Foo superLongParam="bar"
       anotherSuperLongParam="baz" />

  // good, 有多行属性的话, 新建一行关闭标签
  <Foo
    superLongParam="bar"
    anotherSuperLongParam="baz"
  />

  // 若能在一行中显示, 直接写成一行
  <Foo bar="bar" />

  // 子元素按照常规方式缩进
  <Foo
    superLongParam="bar"
    anotherSuperLongParam="baz"
  >
    <Quux />
  </Foo>
  ```

## [Quotes 单引号还是双引号]

- 对于 JSX 属性值总是使用双引号(`"`), 其他均使用单引号(`'`). eslint: [`jsx-quotes`](http://eslint.org/docs/rules/jsx-quotes)

  > 为什么? HTML 属性也是用双引号, 因此 JSX 的属性也遵循此约定.

  ```jsx
  // bad
  <Foo bar='bar' />

  // good
  <Foo bar="bar" />

  // bad
  <Foo style={{ left: "20px" }} />

  // good
  <Foo style={{ left: '20px' }} />
  ```

## [Spacing 空格]

- 总是在自动关闭的标签前加一个空格，正常情况下也不需要换行. eslint: [`no-multi-spaces`](http://eslint.org/docs/rules/no-multi-spaces), [`react/jsx-tag-spacing`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-tag-spacing.md)

  ```jsx
  // bad
  <Foo/>

  // very bad
  <Foo                 />

  // bad
  <Foo
   />

  // good
  <Foo />
  ```

- 不要在 JSX `{}` 引用括号里两边加空格. eslint: [`react/jsx-curly-spacing`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-curly-spacing.md)

  ```jsx
  // bad
  <Foo bar={ baz } />

  // good
  <Foo bar={baz} />
  ```

## [Props 属性]

- JSX 属性名使用骆驼式风格`camelCase`.

  ```jsx
  // bad
  <Foo
    UserName="hello"
    phone_number={12345678}
  />

  // good
  <Foo
    userName="hello"
    phoneNumber={12345678}
  />
  ```

- 如果属性值为 `true`, 可以直接省略. eslint: [`react/jsx-boolean-value`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-boolean-value.md)

  ```jsx
  // bad
  <Foo
    hidden={true}
  />

  // good
  <Foo
    hidden
  />

  // good
  <Foo hidden />
  ```

- <img>  标签总是添加  alt  属性. 如果图片以 presentation(感觉是以类似 PPT 方式显示?)方式显示，alt  可为空, 或者<img>  要包含 role="presentation". eslint: jsx-a11y/alt-text

- 不要在 `alt` 值里使用如 "image", "photo", or "picture"包括图片含义这样的词， 中文也一样. eslint: [`jsx-a11y/img-redundant-alt`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/img-redundant-alt.md)

  > 为什么? 屏幕助读器已经把 `img` 标签标注为图片了, 所以没有必要再在 `alt` 里说明了.

  ```jsx
  // bad
  <img src="hello.jpg" alt="Picture of me waving hello" />

  // good
  <img src="hello.jpg" alt="Me waving hello" />
  ```

- 使用有效正确的 aria `role`属性值 [ARIA roles](https://www.w3.org/TR/wai-aria/roles#usage_intro). eslint: [`jsx-a11y/aria-role`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/aria-role.md)

  ```jsx
  // bad - not an ARIA role
  <div role="datepicker" />

  // bad - abstract ARIA role
  <div role="range" />

  // good
  <div role="button" />
  ```

- 不要在标签上使用 `accessKey` 属性. eslint: [`jsx-a11y/no-access-key`](https://github.com/evcohen/eslint-plugin-jsx-a11y/blob/master/docs/rules/no-access-key.md)

  > 为什么? 屏幕助读器在键盘快捷键与键盘命令时造成的不统一性会导致阅读性更加复杂.

```jsx
// bad
<div accessKey="h" />

// good
<div />
```

- 避免使用数组的 index 来作为属性`key`的值，推荐使用唯一 ID. ([为什么?](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318))

```jsx
// bad
{
  todos.map((todo, index) => <Todo {...todo} key={index} />);
}

// good
{
  todos.map((todo) => <Todo {...todo} key={todo.id} />);
}
```

- 对于所有非必须的属性，总是手动去定义`defaultProps`属性.

  > 为什么? propTypes 可以作为模块的文档说明, 并且声明 defaultProps 的话意味着阅读代码的人不需要去假设一些默认值。更重要的是, 显示的声明默认属性可以让你的模块跳过属性类型的检查.

```jsx
// bad
function SFC({ foo, bar, children }) {
  return (
    <div>
      {foo}
      {bar}
      {children}
    </div>
  );
}
SFC.propTypes = {
  foo: PropTypes.number.isRequired,
  bar: PropTypes.string,
  children: PropTypes.node,
};

// good
function SFC({ foo, bar, children }) {
  return (
    <div>
      {foo}
      {bar}
      {children}
    </div>
  );
}
SFC.propTypes = {
  foo: PropTypes.number.isRequired,
  bar: PropTypes.string,
  children: PropTypes.node,
};
SFC.defaultProps = {
  bar: "",
  children: null,
};
```

- 尽可能少地使用扩展运算符

  > 为什么? 除非你很想传递一些不必要的属性。对于 React v15.6.1 和更早的版本，你可以[给 DOM 传递一些无效的 HTML 属性](https://doc.react-china.org/blog/2017/09/08/dom-attributes-in-react-16.html)

例外情况:

- 使用了变量提升的高阶组件

```jsx
function HOC(WrappedComponent) {
  return class Proxy extends React.Component {
    Proxy.propTypes = {
      text: PropTypes.string,
      isLoading: PropTypes.bool
    };

    render() {
      return <WrappedComponent {...this.props} />
    }
  }
}
```

- 只有在清楚明白扩展对象时才使用扩展运算符。这非常有用尤其是在使用 Mocha 测试组件的时候。

```jsx
export default function Foo {
  const props = {
    text: '',
    isPublished: false
  }

  return (<div {...props} />);
}
```

特别提醒：尽可能地筛选出不必要的属性。同时，使用[prop-types-exact](https://www.npmjs.com/package/prop-types-exact)来预防问题出现。

```jsx
// good
render() {
  const { irrelevantProp, ...relevantProps  } = this.props;
  return <WrappedComponent {...relevantProps} />
}

// bad
render() {
  const { irrelevantProp, ...relevantProps  } = this.props;
  return <WrappedComponent {...this.props} />
}
```

## [Refs]

- 总是在 Refs 里使用回调函数. eslint: [`react/no-string-refs`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-string-refs.md)

  ```jsx
  // bad
  <Foo
    ref="myRef"
  />

  // good
  <Foo
    ref={(ref) => { this.myRef = ref; }}
  />
  ```

## [Parentheses 括号]

- 将多行的 JSX 标签写在 `()`里. eslint: [`react/jsx-wrap-multilines`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-wrap-multilines.md)

  ```jsx
  // bad
  render() {
    return <MyComponent className="long body" foo="bar">
             <MyChild />
           </MyComponent>;
  }

  // good
  render() {
    return (
      <MyComponent className="long body" foo="bar">
        <MyChild />
      </MyComponent>
    );
  }

  // good, 单行可以不需要
  render() {
    const body = <div>hello</div>;
    return <MyComponent>{body}</MyComponent>;
  }
  ```

## [Tags 标签]

- 对于没有子元素的标签来说总是自己关闭标签. eslint: [`react/self-closing-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/self-closing-comp.md)

  ```jsx
  // bad
  <Foo className="stuff"></Foo>

  // good
  <Foo className="stuff" />
  ```

- 如果模块有多行的属性， 关闭标签时新建一行. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

  ```jsx
  // bad
  <Foo
    bar="bar"
    baz="baz" />

  // good
  <Foo
    bar="bar"
    baz="baz"
  />
  ```

## [Methods 函数]

- 使用箭头函数来获取本地变量.

  ```jsx
  function ItemList(props) {
    return (
      <ul>
        {props.items.map((item, index) => (
          <Item
            key={item.key}
            onClick={() => doSomethingWith(item.name, index)}
          />
        ))}
      </ul>
    );
  }
  ```

- 当在 `render()` 里使用事件处理方法时，提前在构造函数里把 `this` 绑定上去. eslint: [`react/jsx-no-bind`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-no-bind.md)

  > 为什么? 在每次 `render` 过程中， 再调用 `bind` 都会新建一个新的函数，浪费资源.

  ```jsx
  // bad
  class extends React.Component {
    onClickDiv() {
      // do stuff
    }

    render() {
      return <div onClick={this.onClickDiv.bind(this)} />;
    }
  }

  // good
  class extends React.Component {
    constructor(props) {
      super(props);

      this.onClickDiv = this.onClickDiv.bind(this);
    }

    onClickDiv() {
      // do stuff
    }

    render() {
      return <div onClick={this.onClickDiv} />;
    }
  }
  ```

- 在 React 模块中，不要给所谓的私有函数添加 `_` 前缀，本质上它并不是私有的.

  > 为什么？`_` 下划线前缀在某些语言中通常被用来表示私有变量或者函数。但是不像其他的一些语言，在 JS 中没有原生支持所谓的私有变量，所有的变量函数都是共有的。尽管你的意图是使它私有化，在之前加上下划线并不会使这些变量私有化，并且所有的属性（包括有下划线前缀及没有前缀的）都应该被视为是共有的。了解更多详情请查看 Issue [#1024](https://github.com/airbnb/javascript/issues/1024), 和 [#490](https://github.com/airbnb/javascript/issues/490) 。

  ```jsx
  // bad
  React.createClass({
    _onClickSubmit() {
      // do stuff
    },

    // other stuff
  });

  // good
  class extends React.Component {
    onClickSubmit() {
      // do stuff
    }

    // other stuff
  }
  ```

- 在 `render` 方法中总是确保 `return` 返回值. eslint: [`react/require-render-return`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/require-render-return.md)

  ```jsx
  // bad
  render() {
    (<div />);
  }

  // good
  render() {
    return (<div />);
  }
  ```

## [Ordering React 模块生命周期]

- `class extends React.Component` 的生命周期函数:

1. 可选的 `static` 方法
2. `constructor` 构造函数
3. `getChildContext` 获取子元素内容
4. `componentWillMount` 模块渲染前
5. `componentDidMount` 模块渲染后
6. `componentWillReceiveProps` 模块将接受新的数据
7. `shouldComponentUpdate` 判断模块需不需要重新渲染
8. `componentWillUpdate` 上面的方法返回 `true`， 模块将重新渲染
9. `componentDidUpdate` 模块渲染结束
10. `componentWillUnmount` 模块将从 DOM 中清除, 做一些清理任务
11. _点击回调或者事件处理器_ 如 `onClickSubmit()` 或 `onChangeDescription()`
12. _`render` 里的 getter 方法_ 如 `getSelectReason()` 或 `getFooterContent()`
13. _可选的 render 方法_ 如 `renderNavigation()` 或 `renderProfilePicture()`
14. `render` render() 方法

- 如何定义 `propTypes`, `defaultProps`, `contextTypes`, 等等其他属性...

  ```jsx
  import React from "react";
  import PropTypes from "prop-types";

  const propTypes = {
    id: PropTypes.number.isRequired,
    url: PropTypes.string.isRequired,
    text: PropTypes.string,
  };

  const defaultProps = {
    text: "Hello World",
  };

  class Link extends React.Component {
    static methodsAreOk() {
      return true;
    }

    render() {
      return (
        <a href={this.props.url} data-id={this.props.id}>
          {this.props.text}
        </a>
      );
    }
  }

  Link.propTypes = propTypes;
  Link.defaultProps = defaultProps;

  export default Link;
  ```

- `React.createClass` 的生命周期函数，与使用 class 稍有不同: eslint: [`react/sort-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/sort-comp.md)

1. `displayName` 设定模块名称
2. `propTypes` 设置属性的类型
3. `contextTypes` 设置上下文类型
4. `childContextTypes` 设置子元素上下文类型
5. `mixins` 添加一些 mixins
6. `statics`
7. `defaultProps` 设置默认的属性值
8. `getDefaultProps` 获取默认属性值
9. `getInitialState` 或者初始状态
10. `getChildContext`
11. `componentWillMount`
12. `componentDidMount`
13. `componentWillReceiveProps`
14. `shouldComponentUpdate`
15. `componentWillUpdate`
16. `componentDidUpdate`
17. `componentWillUnmount`
18. _clickHandlers or eventHandlers_ like `onClickSubmit()` or `onChangeDescription()`
19. _getter methods for `render`_ like `getSelectReason()` or `getFooterContent()`
20. _Optional render methods_ like `renderNavigation()` or `renderProfilePicture()`
21. `render`
