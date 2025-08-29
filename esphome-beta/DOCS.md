# ESPHome 插件

## 安装

此插件的安装非常简单，与安装其他 Home Assistant 插件并无不同。

1. 在 Supervisor 插件商店中搜索 “ESPHome” 插件。
2. 点击 **安装** 按钮，下载并解压插件到你的设备上。这个过程可能需要一些时间。
3. 可选：如果你使用 SSL/TLS 证书并希望加密与该插件的通信，请在 `ssl` 字段中输入 `true`，并相应设置 `fullchain` 和 `certfile` 选项。
4. 启动插件，检查插件日志确认一切正常。
5. 点击 **OPEN WEB UI** 打开 ESPHome 控制面板。你需要使用 Home Assistant 的账号登录——ESPHome 使用 Home Assistant 的认证系统进行登录。

你可以在 [ESPHome 官方文档](https://esphome.io/) 查看更多信息。

## 配置

**注意**：*更改配置后，请记得重启插件。*

插件配置示例：

```json
{
  "ssl": false,
  "certfile": "fullchain.pem",
  "keyfile": "privkey.pem"
}
```

### 选项：`ssl`

启用或禁用与该插件 Web 服务器的加密 SSL/TLS（HTTPS）连接。
设置为 `true` 可加密通信，`false` 则不加密。
请注意，如果设置为 `true`，你还必须生成用于加密的密钥和证书文件，例如使用 [Let's Encrypt](https://www.home-assistant.io/addons/lets_encrypt/) 或 [自签名证书](https://www.home-assistant.io/docs/ecosystem/certificates/tls_self_signed_certificate/)。

### 选项：`certfile`

用于 SSL 的证书文件。如果该文件不存在，插件将无法启动。

**注意**：该文件 **必须** 存放在 `/ssl/`，这是 Home Assistant 的默认路径。

### 选项：`keyfile`

用于 SSL 的私钥文件。如果该文件不存在，插件将无法启动。

**注意**：该文件 **必须** 存放在 `/ssl/`，这是 Home Assistant 的默认路径。

### 选项：`leave_front_door_open`

在插件配置中添加此选项并设置为 `true`，可以禁用认证。

### 选项：`relative_url`

将 ESPHome 控制面板托管在相对 URL 下，这样可以集成到现有的 Web 代理（如 NGINX）中。默认值为 `/`。

### 选项：`status_use_ping`

默认情况下，控制面板使用 mDNS 检查节点是否在线。
如果跨子网使用，除非路由器支持 mDNS 转发或 Avahi，否则该方法无效。

设置为 `true` 将让 ESPHome 使用 ICMP Ping 请求获取节点状态。如果所有节点即使在线也总是显示离线，请使用此选项。

### 选项：`streamer_mode`

设置为 `true` 将启用流媒体模式，使 ESPHome 隐藏所有潜在的敏感信息，例如 WiFi (B)SSID（可能用于定位）、用户名等。
请注意，在 YAML 文件中使用 `!secret` 标签可防止这些信息在编辑和验证时显示。
