# Debug

## Node

目前 node 项目，例如 `wsc-pc-vis` 都是使用 `astroboy-cli` 的 `ast` 命令来启动的，例如 `wsc-pc-vis` 的启动命令如下：

```bash
# qa
ast dev --env qa --mock

# pre
NODE_TETHER=tether-proxy.xxx.com ENABLE_CDN=true ast dev --mock --env pre
```

这个在 debug 的时候是非常不方便的，虽然也可以通过使用 `node app/app.js` 来启动应用，但这样就会失去 reload 等能力，还要设置复杂的环境变量。

庆幸的是 node 和 vscode 提供了 [Inspector] 和 [attach](https://code.visualstudio.com/docs/editor/debugging#_launch-versus-attach-configurations) 的能力，我们可以使用这个能力可以很方便的 debug 代码，下面来看一下：

#### 1、在控制台用 Inspector 模式启动 Node：

```bash
# qa
ast dev --env qa --mock --inspect

# pre
NODE_TETHER=tether-proxy.xxx.com ENABLE_CDN=true ast dev --mock --env pre --inspect
```

后面 make 命令会直接支持 `--inspect`，目前还需要手动加 `--inspect`。

按照如上命令启动项目，会输出如下两行：

```bash
Debugger listening on ws://127.0.0.1:9229/5105300c-50d5-4bd8-864c-b714246d3e11
For help see https://nodejs.org/en/docs/inspector
```

其中 `9229` 就是 debug 的调试端口，是一个 websocket 连接，在 `vscode` 等编辑器里可以 attach 这个端口来调试。

- 注意：预发环境下需要在 zanproxy 配置 `*.pre.s.xxx.com` 为 `192.168.66.240`，否则会有接口报错
- admin 账号下不能在本地运行

#### 2、vscode dubugger 配置

在根目录的 `.vscode/launch.json` 下配置如下：

```json
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "attach",
      "name": "wsc-pc-vis",
      "port": 9229,
      "restart": true
    }
  ]
}
```

配置项的意义如下：

- `type: node`，表面这是一个 node 程序的 debugger;
- `request: attach`：表面这是 Inspector 模式的调试；
- `port: 9229`：这个是 node 在 Inspector 模式下的调试端口号；
- `restart: true`：这是在 node 服务重新启动时重新启动 debugger 服务;

然后就能愉快的 debug 了，可以代理 daily、qa 和 pre，代码改动后也会自动重启。

### Auto Attach

vscode 支持 [auto-attach](https://code.visualstudio.com/blogs/2018/07/12/introducing-logpoints-and-auto-attach)，可以更简单的来 attach debugger。

首先 `command+shift+p`，选择 `Debug: Toggle Auto Attach`，会生成 `.vscode/settings.json` 文件，内容如下：

```json
{
  "debug.node.autoAttach": "on"
}
```

然后在控制台用 Inspector 模式启动 Node 就会自动 debug。
