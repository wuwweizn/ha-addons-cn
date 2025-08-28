# Home Assistant 插件：Piper

## 安装

按照以下步骤在你的系统上安装此插件：

1. 在 Home Assistant 前端导航到 **设置** -> **插件** -> **插件商店**。
2. 找到 “Piper” 插件并点击它。
3. 点击 “安装” 按钮。

## 使用方法

安装并运行此插件后，Home Assistant 中的 Wyoming 集成会自动发现它。要完成设置，点击以下按钮：

[![打开你的 Home Assistant 实例并开始设置新集成](https://my.home-assistant.io/badges/config_flow_start.svg)](https://my.home-assistant.io/redirect/config_flow_start/?domain=wyoming)

或者，你也可以手动安装 Wyoming 集成，详情请参阅 [Wyoming 集成文档](https://www.home-assistant.io/integrations/wyoming/)。

## 配置

### 选项：`voice`

[试听语音示例](https://rhasspy.github.io/piper-samples/)

要使用的 Piper 语音名称，例如 `en_US-lessac-medium`（默认值）。语音模型会自动从 [Hugging Face Piper 语音库](https://huggingface.co/rhasspy/piper-voices/tree/v1.0.0) 下载。

语音名称格式为 `<language>_<REGION>-<name>-<quality>`
其中 `<name>` 来自训练语音的数据集，或者如果提供了，则使用说话者的名字。

语音质量分为四个等级：

* `x_low` - 16kHz，最小/最快
* `low` - 16kHz，快
* `medium` - 22.05kHz，稍慢但音质更好
* `high` - 22.05kHz，最慢但音质最佳

在 Raspberry Pi 4 上，`medium` 及以下模型可以以可用速度运行。如果音质不是优先考虑，建议使用 `low` 或 `x-low` 语音，它们明显比 `medium` 更快。

### 选项：`speaker`

如果语音支持多说话者，可指定使用的说话者编号，例如 [`en-us-libritts-high`](https://rhasspy.github.io/piper-samples/#en-us-libritts-high)。

默认情况下，使用第一个说话者（说话者 0）。

### 选项：`length_scale`

调节语音播放速度。1.0 表示使用语音默认说话速度，<1.0 更快，>1.0 更慢。

### 选项：`noise_scale`

控制音频生成时加入噪声以产生变化的程度。效果高度依赖于语音本身，通常 0 表示没有变化，超过 1 会开始降低音质。

### 选项：`noise_w`

控制说话节奏（音素宽度）的变化。效果高度依赖于语音本身，通常 0 表示无变化，超过 1 会产生明显的卡顿和停顿。

### 选项：`max_piper_procs`

同时运行的 Piper 进程数量（默认 1）。每个 Piper 进程会将一个语音模型加载到内存中，因此同时使用多种语音时需要：

* 根据使用情况启动/停止 Piper 进程，或
* 运行更多 Piper 进程

此插件会为每个请求的语音启动一个 Piper 进程，最多 `max_piper_procs` 个。超过后，最近最少使用的语音将被停止。
如果需要快速切换多种语音，请增加 `max_piper_procs`，但请注意会增加插件的内存占用。

### 选项：`update_voices`

每次插件启动时自动下载新的语音列表。要查看新语音，需要在 Home Assistant 中重新加载 Piper 的 Wyoming 集成。

### 选项：`streaming`

启用音频流支持。按句子边界分割文本，并在生成音频的同时进行播放。需要至少 HA 2025.7。

### 选项：`debug_logging`

在插件日志中打印 DEBUG 级别信息。

## 自定义语音

将自定义语音文件添加到 `/share/piper` 目录。每个自定义语音必须包含模型文件 (`<voice>.onnx`) 和配置文件 (`<voice>.onnx.json`)。
详情请参阅 [训练指南](https://github.com/rhasspy/piper/blob/master/TRAINING.md) 学习如何训练和导出自定义语音。

## 支持

有问题？可以通过以下方式获取帮助：

* [Home Assistant Discord 聊天服务器][discord]
* Home Assistant [社区论坛][forum]
* 加入 Reddit 子版块 [r/homeassistant][reddit]

如果发现 bug，请 [在 GitHub 上提交 issue][issue]。

[discord]: https://discord.gg/c5DvZ4e
[forum]: https://community.home-assistant.io
[issue]: https://github.com/home-assistant/addons/issues
[reddit]: https://reddit.com/r/homeassistant
[repository]: https://github.com/hassio-addons/repository
