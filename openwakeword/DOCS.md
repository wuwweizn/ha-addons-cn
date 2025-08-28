# Home Assistant 插件：openWakeWord

## 安装

按照以下步骤在你的系统上安装此插件：

1. 在 Home Assistant 前端导航到 **设置** -> **插件** -> **插件商店**。
2. 找到 “openWakeWord” 插件并点击它。
3. 点击 “安装” 按钮。

## 使用方法

安装并运行此插件后，Home Assistant 中的 Wyoming 集成将自动发现它。要完成设置，请点击以下按钮：

[![打开你的 Home Assistant 实例并开始设置新的集成](https://my.home-assistant.io/badges/config_flow_start.svg)](https://my.home-assistant.io/redirect/config_flow_start/?domain=wyoming)

或者，你也可以手动安装 Wyoming 集成，详情请参考 [Wyoming 集成文档](https://www.home-assistant.io/integrations/wyoming/)。

## 配置

### 选项：`threshold`

激活阈值（0-1），数值越高表示激活次数越少。参见触发级别了解激活次数与唤醒词检测之间的关系。

### 选项：`trigger_level`

在检测被注册之前需要的激活次数。触发级别越高，检测次数越少。

### 选项：`debug_logging`

启用调试日志。可用于查看卫星连接情况以及每次唤醒词检测的日志信息。

## 自定义唤醒词模型

插件会自动从 `/share/openwakeword` 目录加载自定义唤醒词模型。可 [安装 Samba 插件](https://www.home-assistant.io/common-tasks/supervised/#installing-and-using-the-samba-add-on) 将唤醒词模型文件（`*.tflite`）复制到此目录。

将新模型添加到 `/share/openwakeword` 后，请确保重新加载 openWakeWord 的 Wyoming 集成。重新加载后，新唤醒词将在语音助手设置页面中可供选择。

## 支持

有问题吗？你有多种方式获取帮助：

* [Home Assistant Discord 聊天服务器][discord]
* Home Assistant [社区论坛][forum]
* 加入 Reddit [/r/homeassistant][reddit] 讨论区

如果发现 bug，请在我们的 GitHub 上 [提交 issue][issue]。

[discord]: https://discord.gg/c5DvZ4e
[forum]: https://community.home-assistant.io
[issue]: https://github.com/home-assistant/addons/issues
[reddit]: https://reddit.com/r/homeassistant
[repository]: https://github.com/hassio-addons/repository
