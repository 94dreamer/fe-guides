## 现状：

1、iron 框架，对于 post、put 这类会写数据库的请求，默认会转义；get 请求默认不转义。

2、部分 iron & 前端基于 backbone 的页面（如大部分卖家版 PC 的页面），输入框如果填入 script 标签是会被执行的，但不会被保存（参考第 1 点）。

3、新的基于 react 的页面不会有这种问题，因为框架本身做了。

## 要求：

对于用户输入的内容 或者 来自第三方的内容，需要展示到浏览器里的，必须转义。

## 操作指引：

前端部分（后端同学可略过）：

- 纯 js 代码里，使用 [zenjs] 里的 escape 和 unescape 方法
- jquery 和 zepto 里的 text 方法可以很安全地往节点插入字符串，会自动转义
- backbone 的 underscore 模板，展示数据的时候，使用<%- … %> 转义里面的内容（尤其是用户输入的）。
- 对 model 取值的时候，使用 [model.escape](http://backbonejs.org/#Model-escape)
- react 框架本身已经做了 escape，如果对于确定安全的字符串要原样输出，可以使用 [dangerouslySetInnerHTML](https://facebook.github.io/react/docs/dom-elements.html#dangerouslysetinnerhtml)

后端：

- iron 里 php 模板 或 php 的 controller 部分，使用 Filter::xss($xxxx) 来转义，另外还有一个 htmlspecialchars 方法，会把所有的 html 字符都转义掉，这是更彻底的。
- 有赞自己的 node 框架的项目：@kk
- zanphp 项目里：@周星星
- java 项目：
