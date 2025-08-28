# ESPHome 开发版插件

这是 ESPHome 插件的 **开发版本**。

如果你要部署生产节点，请使用正式版插件。

此插件使用每天 UTC 时间 02:00 自动构建的 ESPHome 版本，用于测试开发中的组件。请参阅下面的 `esphome_fork` 配置以正确设置插件。更新配置后，请确保重建镜像。

## 配置

**注意**：*修改配置后请记得重启插件。*

### 选项：`esphome_fork`

从 fork 或分支安装 ESPHome。
例如，要测试某个 Pull Request，可使用 `pull/XXXX/head`，其中 `XXXX` 为 PR 编号；
或者你可以指定 fork 拥有者的用户名和分支名，如 `username:branch`，前提是仓库仍命名为 `esphome`。

如果你想在镜像更新前测试 dev 分支的最新提交，可以在此输入 `dev`。

请注意，你使用的 fork 或分支 **必须** 与 ESPHome dev 分支保持同步，否则插件 **无法启动**。

## 通用 ESPHome 插件配置

通用选项在其他版本中同样可用。

### 选项：`ssl`

启用或禁用该插件 Web 服务器的加密 SSL/TLS（HTTPS）连接。
设置为 `true` 开启加密，`false` 则关闭。
注意，如果开启加密，你必须生成对应的密钥和证书文件，例如使用 [Let's Encrypt](https://www.home-assistant.io/addons/lets_encrypt/) 或 [自签名证书](https://www.home-assistant.io/docs/ecosystem/certificates/tls_self_signed_certificate/)。

### 选项：`certfile`

用于 SSL 的证书文件。如果该文件不存在，插件将无法启动。

**注意**：文件必须存放在 `/ssl/` 下，这是 Home Assistant 的默认路径。

### 选项：`keyfile`

用于 SSL 的私钥文件。如果该文件不存在，插件将无法启动。

**注意**：文件必须存放在 `/ssl/` 下，这是 Home Assistant 的默认路径。

### 选项：`leave_front_door_open`

将此选项设置为 `true` 可禁用认证。

### 选项：`relative_url`

在相对 URL 下托管 ESPHome 仪表盘，以便集成到现有 Web 代理（如 NGINX）。默认值为 `/`。

### 选项：`status_use_ping`

仪表盘默认使用 mDNS 检查节点是否在线。
如果跨子网使用 mDNS，除非路由器支持 mDNS 转发或 avahi，否则无法正常工作。

设置为 `true` 后，ESPHome 将使用 ICMP ping 请求获取节点状态。适用于节点总是显示离线的情况。

### 选项：`streamer_mode`

设置为 `true` 可启用“主播模式”，隐藏所有潜在的私人信息，例如 WiFi (B)SSID（可能用于定位）、用户名等。
请注意，你需要在 YAML 文件中使用 `!secret` 标签，防止在编辑和验证时显示这些信息。
