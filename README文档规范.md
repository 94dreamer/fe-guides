针对项目和组件有以下两种不同的 README 格式

项目

# Project Title 项目名称

=========================

> 简单描述这个项目是什么

## 相关文档

[PRD 文档]()、[交互稿]()、[设计稿]()、[测试用例]()、[需求变更记录]()

## 项目成员

- 产品 @xxx
- 设计 @xxx
- PM @xxx
- 前端 @xxx
- Reviewer @xxx
- 后端 @xxx
- 测试 @xxx

## 入口

- xxx -- xxx
- xxx -- xxx

## TODO

- [x] xxx 功能需要 xxx 优化 @xxx

  xxx 功能是 xxx 实现的，有 xxx 问题，需要 xxx 支持优化

- [ ] xxx 功能有 xx 问题 @xxx

## 目录结构

\```
.
├── README.md # 说明文件
└── index.ts # 入口文件
\```

## Change Log

### feat: 第一次发布(2019/01/11)

- xxx1 功能 @xxx
- xxx2 功能 @xxx

### feat: 添加 xxx 功能(2019/02/22)

- 在 xxx 页面新增了 xxx 功能 [效率]() @xxx

### fix: 修复 xxx 的问题

- 在 xxx 情况下有 xxx 的问题 @xxx

组件

# Component Title 组件名称

=========================

> Owner @xxx

简单描述这个组件的作用

## 使用方式

\```js
import ReactDOM from 'react-dom';

import { createRouter } from 'fns/router';

const routes = [...];
const Routes = createRouter(routes);

ReactDOM.render(Routes, document.getElementById('#app'));
\```

`createRouter` 的参数类型是 `IVisRoutes[]`:

\```ts
import { RouteProps } from 'react-router';

interface IVisRoutes extends RouteProps {
children?: IVisRoutes[]; // 子路由
redirect?: string; // 重定向的路由
index?: string; // IndexRedirect 子路由
breadcrumb?: string | IVisBreadcrumb | ((nextState: RouterState) => string | IVisBreadcrumb); // 面包屑
}

interface IVisBreadcrumb {
project?: string | { name: string; href?: string };
page?: string;
}
\```

### API

| 参数 | 说明       | 类型   | 默认值 | 是否必填 |
| ---- | ---------- | ------ | ------ | -------- |
| path | 匹配的路径 | string | noop   | 是       |

## Change Log

### feat: 第一次发布(2019/01/11)

- xxx1 功能 @xxx
- xxx2 功能 @xxx

### feat: 添加 xxx 功能(2019/02/22)

- 新增了 xxx 功能 [效率]() @xxx

### fix: 修复 xxx 的问题

- 在 xxx 情况下有 xxx 的问题 @xxx

## TODO

- [x] xxx 功能需要 xxx 优化 @xxx

  xxx 功能是 xxx 实现的，有 xxx 问题，需要 xxx 支持优化

- [ ] xxx 功能有 xx 问题 @xxx
