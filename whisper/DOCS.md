# Home Assistant 插件：Whisper

---

## 安装

按照以下步骤在系统中安装该插件：

1. 在 Home Assistant 前端，进入 **设置 (Settings)** -> **插件 (Add-ons)** -> **插件商店 (Add-on store)**。
2. 找到 “Whisper” 插件并点击它。
3. 点击 “安装 (INSTALL)” 按钮。

---

## 使用方法

插件安装并运行后，Home Assistant 的 Wyoming 集成会自动发现它。要完成设置，请点击以下按钮：

[![在 Home Assistant 中打开并开始设置新集成](https://my.home-assistant.io/badges/config_flow_start.svg)](https://my.home-assistant.io/redirect/config_flow_start/?domain=wyoming)

或者，你也可以手动安装 Wyoming 集成，详情请参见 [Wyoming 集成文档](https://www.home-assistant.io/integrations/wyoming/)。

---

## 配置

### 选项：`language`

插件默认语言。Home Assistant 2023.8 及以上版本，不同 [Assist pipelines](https://www.home-assistant.io/voice_control/voice_remote_local_assistant/) 可以同时使用多种语言。

选择 “auto” 时，模型运行会**明显更慢**，但可以自动检测语音语言。

* [支持语言性能](https://github.com/openai/whisper#available-models-and-languages)
* [两字母语言代码列表](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)

---

### 选项：`model`

Whisper 转录模型。选择 `custom` 时，使用 `custom_model` 指定的模型，可为 HuggingFace 模型 ID，例如 `"Systran/faster-distil-whisper-small.en"`。

默认模型为 `auto`：

* ARM 设备（如 Raspberry Pi 4）使用 `tiny-int8`
* 其他设备使用 `base-int8`

`int8` 压缩模型比普通模型略不精确，但体积小、速度快。
[Distilled 模型](https://github.com/huggingface/distil-whisper)未压缩，但比原始模型更快更小。

可用模型列表：

* `auto` (根据 CPU 自动选择)
* `tiny-int8` (压缩)
* `tiny`
* `tiny.en` (仅英文)
* `base-int8` (压缩)
* `base`
* `base.en` (仅英文)
* `small-int8` (压缩)
* `distil-small.en` (蒸馏版，仅英文)
* `small`
* `small.en` (仅英文)
* `medium-int8` (压缩)
* `distil-medium.en` (蒸馏版，仅英文)
* `medium`
* `medium.en` (仅英文)
* `large`
* `large-v1`
* `distil-large-v2` (蒸馏版，仅英文)
* `large-v2`
* `distil-large-v3` (蒸馏版，仅英文)
* `large-v3`
* `turbo` (比 `large-v3` 更快)

---

### 选项：`custom_model`

指定本地转换后的模型目录路径，或 HuggingFace Hub 的 CTranslate2 Whisper 模型 ID，例如 `"Systran/faster-distil-whisper-small.en"`。

如果 `custom_model_type` 设置为 `transformers`，则必须使用 HuggingFace transformers Whisper 模型 ID，例如 `"openai/whisper-tiny.en"`。

**使用本地自定义模型步骤**：

1. 在插件配置目录下创建 `models` 子目录（若不存在）。
2. 将模型目录复制到：`/addon_configs/core_whisper/models/<你的模型目录>`
3. 设置 `custom_model` 路径为：`/config/models/<你的模型目录>`

> 本地模型路径必须以 `/config/models/` 开头，插件通过挂载卷访问 Home Assistant 配置目录。

---

### 选项：`custom_model_type`

* `faster-whisper`（默认）
* `transformers`

若设置为 `transformers`，`custom_model` 必须为 HuggingFace transformers Whisper 模型，如 `"openai/whisper-tiny.en"`。

**注意**：目前 transformers 模型不支持 initial prompt。

---

### 选项：`beam_size`

转录时同时考虑的候选数量（参考 [beam search](https://en.wikipedia.org/wiki/Beam_search)）。
默认值 `0` 会自动选择：

* ARM 设备（如 Raspberry Pi 4）为 1
* 其他设备为 5

增加 beam size 可以提升准确率，但会降低性能。

---

### 选项：`initial_prompt`

对音频的描述，可以帮助 Whisper 更好地识别不常见词汇。
示例参考 [讨论链接](https://github.com/openai/whisper/discussions/963)。

---

## 备份

Whisper 模型文件通常较大，因此默认不包含在备份中，恢复后远程模型会重新下载。
如果使用本地自定义模型，恢复备份后需手动再次复制模型目录。

---

## 支持

如有疑问，可通过以下方式获取帮助：

* [Home Assistant Discord 聊天服务器][discord]
* [Home Assistant 社区论坛][forum]
* [Reddit /r/homeassistant][reddit]

发现问题可 [在 GitHub 上开 issue][issue]。

[discord]: https://discord.gg/c5DvZ4e
[forum]: https://community.home-assistant.io
[issue]: https://github.com/home-assistant/addons/issues
[reddit]: https://reddit.com/r/homeassistant
[repository]: https://github.com/hassio-addons/repository


