
# Home Assistant 社区插件：Node-RED

[Node-RED][nodered] 是一个用于将硬件设备、API 和在线服务以新颖方式连接在一起的编程工具。

它提供了一个**基于浏览器的编辑器**，可以使用调色板中丰富的节点轻松构建流程，并通过一次点击将其部署到运行时环境中。

## 安装

安装此插件非常简单，与安装其他 Home Assistant 插件没有区别。

1. 点击下面的 Home Assistant 按钮，在你的 Home Assistant 实例中打开插件。

   [![在你的 Home Assistant 实例中打开此插件][addon-badge]][addon]

2. 点击“安装”按钮安装插件。

3. 启动“Node-RED”插件。

4. 检查“Node-RED”日志，确保一切正常。

5. 点击“打开网页界面”按钮进入 Node-RED。

6. 插件开箱即用！无需配置服务器！

**注意**：插件**已预配置**，无需添加、修改或更新服务器连接设置！

## 配置

**注意**：*当配置更改后，请记得重启插件。*

示例插件配置：

```yaml
log_level: info
http_node:
  username: MarryPoppins
  password: Supercalifragilisticexpialidocious
http_static:
  username: MarryPoppins
  password: Supercalifragilisticexpialidocious
ssl: true
certfile: fullchain.pem
keyfile: privkey.pem
system_packages:
  - ffmpeg
npm_packages:
  - node-red-admin
init_commands:
  - echo 'This is a test'
  - echo 'So is this...'
```

**注意**：*这只是示例，请不要直接复制粘贴！请创建自己的配置！*

### 选项：`log_level`

`log_level` 选项控制插件日志输出的详细程度，可根据需要调整，便于排查未知问题。可能的值包括：

* `trace`：显示每个细节，包括所有内部函数调用。
* `debug`：显示详细调试信息。
* `info`：普通（通常）有用事件。
* `warning`：非错误的异常情况。
* `error`：运行时错误，不需要立即处理。
* `fatal`：严重错误，插件无法使用。

请注意，每个级别会自动包含更严重级别的日志信息，例如 `debug` 也会显示 `info` 消息。默认 `log_level` 为 `info`，这是推荐设置，除非你正在排查问题。

### 选项：`ssl`

启用/禁用网页界面的 SSL（HTTPS）。设置为 `true` 启用，为 `false` 禁用。

**注意**：*SSL 设置仅适用于直接访问，对 Ingress 服务无效。*

### 选项：`certfile`

用于 SSL 的证书文件。

**注意**：*文件必须存放在 `/ssl/`，这是默认路径*

### 选项：`keyfile`

用于 SSL 的私钥文件。

**注意**：*文件必须存放在 `/ssl/`，这是默认路径*

### 选项：`credential_secret`

Node-RED 会使用一个密钥对存储的凭证进行加密。此选项允许你指定该密钥，可视作密码。请妥善保存，未来可能需要（如恢复备份时）。

**注意**：*设置此属性后，请勿更改，否则 Node-RED 将无法解密现有凭证，数据将丢失。*
**注意**：*如果你手动启用了 Node-RED 的项目功能，即使必需，此选项也会被忽略。*

### 选项：`theme`

设置 Node-RED 的主题。可用选项包括：

* `default`、`aurora`、`cobalt2`、`dark`、`dracula`、`espresso-libre`、`github-dark`、`github-dark-default`、`github-dark-dimmed`、`midnight-red`、`monoindustrial`、`monokai`、`monokai-dimmed`、`noctis`、`oceanic-next`、`oled`、`one-dark-pro`、`one-dark-pro-darker`、`solarized-dark`、`solarized-light`、`tokyo-night`、`tokyo-night-light`、`tokyo-night-storm`、`totallyinformation`、`zenburn`

### 选项：`http_node`

用于给节点定义的 HTTP 端点（`httpNodeRoot`）设置访问保护，可使用以下属性：

* `username`
* `password`

**注意**：*使用 `http_node` 时，需要在 Ingress 之外通过网络端口暴露 Node-RED。HTTP 节点将在 `/endpoint/` 下显示。如果使用 `node-red-dashboard` 模块，也会托管在此路径下，并使用此处设置的凭证。*

### 选项：`http_static`

用于给静态内容（`httpStatic`）设置访问保护，可使用以下属性：

* `username`
* `password`

### 选项：`system_packages`

允许你指定额外的 [Alpine 软件包][alpine-packages] 安装到 Node-RED（如 `g++`、`make`、`ffmpeg`）。

**注意**：*添加过多软件包会延长插件启动时间。*

### 选项：`npm_packages`

允许你指定额外的 [NPM 包][npm-packages] 或 [Node-RED 节点][node-red-nodes] 安装到 Node-RED（如 `node-red-dashboard`、`node-red-contrib-ccu`）。

**注意**：*添加过多软件包会延长插件启动时间。*

### 选项：`init_commands`

使用 `init_commands` 可进一步自定义 Node-RED 环境。添加一个或多个 shell 命令，它们会在每次插件启动时执行。

### 选项：`safe_mode`

设置为 `true` 时，将以 `--safe` 标志启动 Node-RED，不启动任何流程，用于排查问题。

### 选项：`leave_front_door_open`

在插件配置中添加此选项，可通过设置为 `true` 并留空用户名和密码，禁用插件身份验证。

**注意**：*强烈建议不要使用，即使仅在内部网络中暴露。使用风险自负！*

### 选项：`max_old_space_size`

设置 nodeJS V8 老内存区的最大内存（MB）。内存使用接近上限时，V8 会增加垃圾回收以释放未使用内存。

[https://nodejs.org/api/cli.html#--max-old-space-sizesize-in-megabytes](https://nodejs.org/api/cli.html#--max-old-space-sizesize-in-megabytes)

## 配置文件夹

插件会将大部分配置存储在 Node-RED 插件配置文件夹，包括 `flows.json`。

## 时区配置

插件会使用 Home Assistant 中设置的时区。如果时区不正确，请在 Home Assistant 中更新设置并重启 Node-RED 插件。

如果希望单独覆盖 Node-RED 的时区，可在 `settings.js` 文件中配置。

在 `module.exports = {` 行上方添加：

```js
process.env.TZ = "America/Toronto";
```

时区应根据你的环境修改。保存文件并重启 Node-RED 插件。

## 已知问题与限制

* 虽然插件内置 Node-RED Dashboard，但目前**不支持通过 Ingress 访问**。这是 Node-RED Dashboard 的技术限制。
* 如果无法访问 HTTP 节点或 Dashboard，请检查是否在插件“网络”配置中启用了直接访问模式并设置端口。
* 如果无法访问 HTTP 节点或 Dashboard，请检查 URL 是否以 `/endpoint/` 开头，否则 Home Assistant 身份验证将生效。
* 更新后出现以下警告：
  `WARNING (MainThread) [hassio.api.proxy] Unauthorized WebSocket access!`
  请验证 Node-RED 中 Home Assistant 服务器的配置。双击任意 Home Assistant 节点并点击服务器名称旁的铅笔图标。确保勾选 `I use the Home Assistant Add-On`。

## 更新记录与版本发布

本仓库使用 [GitHub Releases][releases] 记录更新日志，格式基于 [Keep a Changelog][keepchangelog]。

版本基于 [语义化版本控制][semver]，格式为 `MAJOR.MINOR.PATCH`，规则如下：

* `MAJOR`：不兼容或重大更改。
* `MINOR`：向后兼容的新功能和增强。
* `PATCH`：向后兼容的 bug 修复和包更新。

## 支持

有问题吗？

你有几种方式可以获得帮助：

* 通过 [Home Assistant Community Add-ons Discord][discord] 获取插件支持和功能请求。
* 通过 [Home Assistant Discord][discord-ha] 进行一般性讨论和问题咨询。
* 在 Home Assistant [社区论坛][forum] 提问。
* 加入 Reddit [/r/homeassistant][reddit] 讨论区。
* 查阅 [Node-RED 官方文档][nodered-docs]。

你也可以在 GitHub [这里开 issue][issue]。

## 作者与贡献者

本仓库最初由 [Franck Nijhof][frenck] 设置。

完整的作者和贡献者列表，请查看 [贡献者页面][contributors]。

## 许可协议

MIT 许可证

版权所有 (c) 2018-2025 Franck Nijhof

特此免费授予任何获得本软件及相关文档文件（“软件”）副本的人无限制使用、复制、修改、合并、发布、分发、再授权和/或出售本软件的权利，并允许向其提供本软件的人在符合以下条件的情况下使用：

以上版权声明和本许可声明必须包含在本软件的所有副本或主要部分中。

本软件按“原样”提供，不附带任何形式的明示或暗示保证，包括但不限于适销性、特定用途适用性及不侵权保证。在任何情况下，作者或版权持有人均不对因软件或软件使用或其他交易产生的任何索赔、损害或其他责任负责，无论是合同、侵权或其他形式。

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_nodered&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[alpine-packages]: https://pkgs.alpinelinux.org/packages
[contributors]: https://github.com/hassio-addons/addon-node-red/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord]: https://discord.me/hassioaddons
[forum]: https://community.home-assistant.io/t/home-assistant-community-add-on-node-red/55023?u=frenck
[frenck]: https://github.com/frenck
[issue]: https://github.com/hassio-addons/addon-node-red/issues
[node-red-nodes]: https://flows.nodered.org/?type=node&num_pages=1
[nodered-docs]: https://nodered.org/docs
[nodered]: https://nodered.org
[npm-packages]: https://www.npmjs.com
[reddit]: https://reddit.com/r/homeassistant
[releases]: https://github.com/hassio-addons/addon-node-red/releases
[semver]: https://semver.org/spec/v2.0.0.html
[keepchangelog]: https://keepachangelog.com

