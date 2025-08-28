# Home Assistant 社区插件：ZeroTier One

[ZeroTier][zerotier] 结合了 VPN、SDN 和 SD-WAN 的功能于一个系统中。它可以让你像管理一个单一数据中心一样，管理所有本地和广域网的连接资源。

用户可以使用 ZeroTier 无缝连接笔记本、台式机、手机、嵌入式设备、云资源和应用，无论身处何地。它将整个世界转变为一个统一的数据中心，现在你可以通过此插件将你的 Home Assistant 实例加入其中。

## 安装

此插件的安装非常简单，与安装其他 Home Assistant 插件类似：

1. 点击下面的 Home Assistant 我的按钮，在你的 Home Assistant 实例中打开插件。

   [![在 Home Assistant 实例中打开此插件][addon-badge]][addon]

2. 点击“Install”按钮安装插件。

3. 在 [zerotier.com][zerotier] 注册免费账户并获取一个网络 ID。

4. 在插件配置中将 `"network_id"` 设置为你的网络 ID。

5. 启动 “ZeroTier One” 插件。

6. 查看插件日志，确认一切正常。

7. 你的实例将会显示在 ZeroTier 账户中。

## 配置

**注意**：*更改配置后请重启插件。*

示例配置：

```yaml
networks:
  - wgfyiwe73747457
  - fhu3888892jjfdk
api_auth_token: ""
```

**注意**：*此示例仅供参考，请根据实际情况创建自己的配置！*

### 配置选项说明

#### `log_level`

控制插件日志输出级别，可根据需要设置详细程度：

* `trace`：显示每一个细节，包括所有内部调用函数。
* `debug`：显示详细调试信息。
* `info`：正常事件（默认）。
* `warning`：异常情况，但非错误。
* `error`：运行时错误，不需要立即处理。
* `fatal`：严重错误，插件不可用。

日志等级会自动包含比它更严重的消息，例如 `debug` 也会显示 `info` 消息。

#### `networks`

配置要加入的网络 ID（VLAN），可在 ZeroTier 账户中找到。

**支持 secrets，例如：** `!secret zerotier_network_id`

#### `api_auth_token`

ZeroTier 提供本地 HTTP JSON API，可通过端口访问，用于查询或控制 ZeroTier 实例。

此令牌类似密码，如果不使用 API 功能可留空。

**支持 secrets，例如：** `!secret zerotier_token`

更多信息可参考 [ZeroTier JSON API 文档][api]。

## 更新日志与版本

本仓库使用 [GitHub Releases][releases] 记录更新。
版本遵循 [语义化版本][semver]，格式为 `MAJOR.MINOR.PATCH`：

* `MAJOR`：重大或不兼容更新。
* `MINOR`：向后兼容的新功能或增强。
* `PATCH`：向后兼容的错误修复或更新。

## 支持

如有问题，可以通过以下途径获取帮助：

* [Home Assistant 社区插件 Discord][discord]（插件支持及功能请求）
* [Home Assistant Discord][discord-ha]（Home Assistant 讨论）
* Home Assistant [社区论坛][forum]
* Reddit [r/homeassistant][reddit]
* GitHub [打开问题][issue]

## 作者及贡献者

原作者：[Franck Nijhof][frenck]
完整贡献者列表：[contributors][contributors]

## 许可协议

MIT License

版权所有 (c) 2019-2025 Franck Nijhof

允许免费使用、复制、修改、合并、发布、分发、再许可及销售软件及文档，须包含版权声明及许可声明。

软件按“原样”提供，不保证任何形式的明示或暗示担保。

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_zerotier&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[api]: https://www.zerotier.com/manual.shtml#4_1
[contributors]: https://github.com/hassio-addons/addon-zerotier/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord]: https://discord.me/hassioaddons
[forum]: https://community.home-assistant.io/t/home-assistant-community-add-on-zerotier-one/109091?u=frenck
[frenck]: https://github.com/frenck
[issue]: https://github.com/hassio-addons/addon-zerotier/issues
[reddit]: https://reddit.com/r/homeassistant
[releases]: https://github.com/hassio-addons/addon-zerotier/releases
[semver]: https://semver.org/spec/v2.0.0.html
[zerotier]: https://www.zerotier.com/
