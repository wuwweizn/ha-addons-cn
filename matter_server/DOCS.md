
# Home Assistant 插件：Matter Server

## 安装

使用以下步骤安装此插件。

1. 点击下面的 **Home Assistant My** 按钮，在你的 Home Assistant 实例中打开插件页面。

   [![在你的 Home Assistant 实例中打开此插件][addon-badge]][addon]

2. 点击 **“安装”** 按钮来安装此插件。

## 使用方法

启动 **Matter Server 插件** 以便 Home Assistant Core 可以使用其 WebSocket。
然后在 Home Assistant Core 中安装 [Matter 集成][matter_integration]。

### 外部访问 WebSocket 接口（高级）

默认情况下，Python Matter Server 的 WebSocket 接口只在内部开放。
你仍然可以通过主机接口启用外部访问：
点击 **“显示已禁用端口”**，并在 **Matter Server WebSocket 服务器端口** 字段中输入一个端口号（例如 **5580**）。

## 配置

插件配置项：

| 配置项                    | 说明                             |
| ---------------------- | ------------------------------ |
| log\_level             | Matter Server 组件的日志级别。         |
| log\_level\_sdk        | Matter SDK 日志的日志级别。            |
| beta                   | 是否在启动时安装最新的 Beta 版本。           |
| enable\_test\_net\_dcl | 启用测试网络的 DCL，用于 PAA 根证书和其他设备信息。 |
| bluetooth\_adapter\_id | 设置 BlueZ 蓝牙控制器 ID（用于本地调试/配网）。  |

## 支持

有问题？你有多种方式获得帮助：

* [Home Assistant Discord 聊天服务器][discord]
* Home Assistant [社区论坛][forum]
* 加入 [Reddit 子论坛][reddit]，在 [/r/homeassistant][reddit] 参与讨论

如果你发现了 Bug，请到 [我们的 GitHub 提交 issue][issue]。

[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=core_matter_server
[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[discord]: https://discord.gg/c5DvZ4e
[forum]: https://community.home-assistant.io
[reddit]: https://reddit.com/r/homeassistant
[issue]: https://github.com/home-assistant/addons/issues
[matter_server_repo]: https://github.com/home-assistant-libs/python-matter-server
[matter_integration]: https://www.home-assistant.io/integrations/matter/


