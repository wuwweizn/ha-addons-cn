# ESPHome 插件

## 安装

此插件的安装过程非常简单，与安装其他 Home Assistant 插件没有区别。

1. 在 Supervisor 插件商店中搜索 “ESPHome” 插件。
2. 点击安装，将插件下载并解压到你的设备上。此过程可能需要一些时间。
3. 可选：如果你使用 SSL/TLS 证书并希望加密与此插件的通信，请在 `ssl` 字段中填写 `true`，并根据需要设置 `fullchain` 和 `certfile` 选项。
4. 启动插件，并查看插件日志以确认是否正常运行。
5. 点击 “OPEN WEB UI” 打开 ESPHome 仪表盘。你需要使用 Home Assistant 的账号登录 —— ESPHome 使用 Home Assistant 的认证系统。

你可以在 [ESPHome 官方文档](https://esphome.io/) 查看详细说明。

## 配置

**注意**：*修改配置后请记得重启插件。*

示例插件配置：

```json
{
  "ssl": false,
  "certfile": "fullchain.pem",
  "keyfile": "privkey.pem"
}
```

### 选项：`ssl`

启用或禁用对插件 Web 服务的 SSL/TLS（HTTPS）加密连接。

* 设置为 `true`：启用加密
* 设置为 `false`：不启用

请注意，如果设置为 `true`，必须生成用于加密的证书和密钥文件，例如使用 [Let's Encrypt](https://www.home-assistant.io/addons/lets_encrypt/) 或 [自签名证书](https://www.home-assistant.io/docs/ecosystem/certificates/tls_self_signed_certificate/)。

### 选项：`certfile`

用于 SSL 的证书文件。如果文件不存在，插件将无法启动。

**注意**：文件必须存储在 `/ssl/` 目录，这是 Home Assistant 的默认路径。

### 选项：`keyfile`

用于 SSL 的私钥文件。如果文件不存在，插件将无法启动。

**注意**：文件必须存储在 `/ssl/` 目录，这是 Home Assistant 的默认路径。

### 选项：`leave_front_door_open`

将此选项设置为 `true` 可以禁用身份验证。

### 选项：`relative_url`

将 ESPHome 仪表盘托管在相对 URL 下，以便可以通过现有的反向代理（如 NGINX）访问。默认值为 `/`。

### 选项：`status_use_ping`

默认情况下，仪表盘使用 mDNS 检测节点是否在线。

* 如果跨子网无法工作（除非路由器支持 mDNS 转发或 Avahi），可将此选项设置为 `true`，使 ESPHome 使用 ICMP Ping 请求获取节点状态。
* 如果所有节点总是显示离线，即使它们已连接，也请启用此选项。

### 选项：`streamer_mode`

设置为 `true` 可启用直播模式，隐藏所有可能的隐私信息，例如 WiFi (B)SSID、用户名等。

* 注意：在 YAML 文件中使用 `!secret` 标签，以防止这些信息在编辑和验证时显示。
