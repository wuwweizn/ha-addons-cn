
# Home Assistant 社区插件：TasmoAdmin

TasmoAdmin（前称 SonWEB）是一个管理 Sonoff-Tasmota 设备的网页管理界面，可集中管理所有设备。主要功能包括：

* 扫描网络并自动添加设备
* 快速查看所有设备的状态
* 从单一界面配置所有设备
* 对一个或多个设备进行 OTA 固件升级
* 可自动下载最新固件

---

## 安装

安装过程与其他 Home Assistant 插件类似，非常简单：

1. 点击下方按钮，在 Home Assistant 中打开该插件：

   [![在 Home Assistant 中打开此插件][addon-badge]][addon]

2. 点击“安装”按钮安装插件。

3. 启动 “TasmoAdmin” 插件。

4. 查看插件日志，确认安装正常。

---

## 配置

**注意**：修改配置后需要重启插件才能生效。

示例配置：

```yaml
log_level: info
ssl: false
certfile: fullchain.pem
keyfile: privkey.pem
```

**注意**：这是示例配置，请根据实际情况创建自己的配置。

### 选项说明

#### `log_level`

控制插件日志输出级别，可用于调试。可能的值包括：

* `trace`：显示所有细节，包括内部函数调用
* `debug`：详细调试信息
* `info`：一般事件（默认）
* `warning`：异常事件，但非错误
* `error`：运行时错误
* `fatal`：严重错误，插件不可用

每个级别会包含比它更严重的日志信息，例如 `debug` 会包含 `info` 信息。默认值为 `info`，推荐用于正常运行。

#### `ssl`

是否启用网页界面的 SSL（HTTPS）。
设置为 `true` 启用，`false` 禁用。

**注意**：Tasmota 不支持通过 HTTPS 进行 OTA。

#### `certfile`

SSL 证书文件路径。

**注意**：文件必须存储在 `/ssl/` 目录下（默认路径）。

#### `keyfile`

SSL 私钥文件路径。

**注意**：文件必须存储在 `/ssl/` 目录下（默认路径）。

---

## 更新日志与版本

本仓库使用 [GitHub Releases][releases] 管理更新日志。

版本遵循 [语义化版本][semver]：

* `MAJOR`：不兼容或重大更改
* `MINOR`：向后兼容的新功能或增强
* `PATCH`：向后兼容的修复或更新

---

## 支持

如有疑问，可通过以下方式获取帮助：

* [Home Assistant 社区插件 Discord][discord]
* [Home Assistant 官方 Discord][discord-ha]
* [Home Assistant 社区论坛][forum]
* [Reddit /r/homeassistant][reddit]
* 在 GitHub [开 issue][issue]

---

## 作者与贡献者

此仓库最初由 [Franck Nijhof][frenck] 创建。
完整贡献者列表请查看 [贡献者页面][contributors]。

---

## 许可证

MIT 许可证

版权所有 (c) 2018-2025 Franck Nijhof

允许在遵守 MIT 许可证的前提下自由使用、修改、发布和分发本软件。

---

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_sonweb&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[contributors]: https://github.com/hassio-addons/addon-tasmoadmin/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord]: https://discord.me/hassioaddons
[forum]: https://community.home-assistant.io/t/home-assistant-community-add-on-tasmoadmin/54155?u=frenck
[frenck]: https://github.com/frenck
[issue]: https://github.com/hassio-addons/addon-tasmoadmin/issues
[reddit]: https://reddit.com/r/homeassistant
[releases]: https://github.com/hassio-addons/addon-tasmoadmin/releases
[semver]: http://semver.org/spec/v2.0.0.html


