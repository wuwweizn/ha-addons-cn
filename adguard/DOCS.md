
# Home Assistant 社区插件：AdGuard Home

[AdGuard Home][adguard] 是一个**网络范围的广告和跟踪器拦截 DNS 服务器**，同时具备**家长控制（成人内容拦截）**功能。它的目的是让你能够**掌控整个网络和所有设备**，并且不需要使用客户端程序。

AdGuard Home 提供了一个**美观、简洁且功能丰富的网页界面**，可以轻松管理过滤流程及相关设置。

## 安装

安装此插件非常简单，与安装任何其他 Home Assistant 插件没有区别。

1. **确保你的 Home Assistant 设备拥有[静态 IP 和静态外部 DNS 服务器](https://github.com/home-assistant/operating-system/blob/dev/Documentation/network.md#static-ip)!**
   这非常重要！如果跳过此步骤，你**肯定会**遇到问题。

   * 在网络设置中修改此项：
     [![打开 Home Assistant 并管理系统网络配置](https://my.home-assistant.io/badges/network.svg)](https://my.home-assistant.io/redirect/network/)
     (*设置 → 系统 → 网络 → 配置网络接口 → 你的接口 → IPv4 → 静态*)
   * 请注意，在路由器中设置固定 IP **不等于静态 IP**。

2. 点击下面的 Home Assistant 按钮，在你的 Home Assistant 实例中打开插件。

   [![在你的 Home Assistant 实例中打开此插件][addon-badge]][addon]

3. 点击“安装”按钮安装插件。

4. 启动“AdGuard Home”插件。

5. 检查“AdGuard Home”日志，确保一切正常。

6. 点击“打开网页界面”按钮，并使用你的 Home Assistant 账户登录。

7. 安装完成，准备使用！

## 配置

**注意**：*当配置更改后，请记得重启插件。*

示例插件配置：

```yaml
log_level: info
ssl: true
certfile: fullchain.pem
keyfile: privkey.pem
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

启用/禁用插件的 SSL（HTTPS）。设置为 `true` 启用，为 `false` 则禁用。

**注意**：*SSL 设置仅适用于直接访问，对 Ingress 服务无效。*

### 选项：`certfile`

用于 SSL 的证书文件。

**注意**：*文件必须存放在 `/ssl/`，这是默认路径*

### 选项：`keyfile`

用于 SSL 的私钥文件。

**注意**：*文件必须存放在 `/ssl/`，这是默认路径*

### 选项：`leave_front_door_open`

在插件配置中添加此选项，可通过设置为 `true` 禁用 AdGuard Home 的身份验证。

**注意**：*强烈建议不要使用，即使此插件仅在内部网络中暴露。使用风险自负！*

## 加密设置（高级用法）

AdGuard 允许配置本地的 DNS-over-HTTPS 和 DNS-over-TLS。如果启用这些选项，请确保之后重启插件。
同时，若要正确使用 DNS-over-HTTPS，请确保在插件和 AdGuard 本身都配置了 SSL，并注意插件与 AdGuard 不能使用相同的 SSL 端口。

## 更新记录与版本发布

本仓库使用 [GitHub Releases][releases] 功能记录更新日志。

版本基于 [语义化版本控制][semver]，格式为 `MAJOR.MINOR.PATCH`。简而言之，版本号更新规则如下：

* `MAJOR`：不兼容或重大更改。
* `MINOR`：向后兼容的新功能和增强。
* `PATCH`：向后兼容的 bug 修复和包更新。

## 支持

有问题吗？

你有几种方式可以获得帮助：

* 通过 [Home Assistant Community Add-ons Discord 服务器][discord] 获取插件支持和功能请求。
* 通过 [Home Assistant Discord 服务器][discord-ha] 进行一般性讨论和问题咨询。
* 在 Home Assistant [社区论坛][forum] 提问。
* 加入 Reddit 的 [/r/homeassistant][reddit] 讨论区。

你也可以在 GitHub [这里开 issue][issue]。

## 作者与贡献者

本仓库最初由 [Franck Nijhof][frenck] 设置。

完整的作者和贡献者列表，请查看 [贡献者页面][contributors]。

## 许可协议

MIT 许可证

版权所有 (c) 2019-2025 Franck Nijhof

特此免费授予任何获得本软件及相关文档文件（“软件”）副本的人无限制使用、复制、修改、合并、发布、分发、再授权和/或出售本软件的权利，并允许向其提供本软件的人在符合以下条件的情况下使用：

以上版权声明和本许可声明必须包含在本软件的所有副本或主要部分中。

本软件按“原样”提供，不附带任何形式的明示或暗示保证，包括但不限于适销性、特定用途适用性及不侵权保证。在任何情况下，作者或版权持有人均不对因软件或软件使用或其他交易产生的任何索赔、损害或其他责任负责，无论是合同、侵权或其他形式。

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_adguard&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[adguard]: https://adguard.com/adguard-home/overview.html
[contributors]: https://github.com/hassio-addons/addon-adguard-home/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord]: https://discord.me/hassioaddons
[forum]: https://community.home-assistant.io/t/home-assistant-community-add-on-adguard-home/90684?u=frenck
[frenck]: https://github.com/frenck
[issue]: https://github.com/hassio-addons/addon-adguard-home/issues
[reddit]: https://reddit.com/r/homeassistant
[releases]: https://github.com/hassio-addons/addon-adguard-home/releases
[semver]: https://semver.org/spec/v2.0.0.html

---
