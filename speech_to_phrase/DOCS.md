
# Home Assistant 插件：语音转指令（Speech to phrase）

---

## 安装

按照以下步骤在系统中安装此插件：

1. 在 Home Assistant 前端，进入 **设置** -> **插件** -> **插件商店**。
2. 找到“语音转指令（Speech to phrase）”插件并点击它。
3. 点击“安装（INSTALL）”按钮。

---

## 使用方法

安装并运行此插件后，它会根据你 \[公开的]\[] 实体、区域、楼层以及 [句子触发器][sentence trigger] 自动训练自己。
如有必要，插件会自动重新训练。

此插件会被 Home Assistant 的 Wyoming 集成自动发现。
完成设置，请点击以下按钮：

[![打开你的 Home Assistant 实例并开始设置新的集成](https://my.home-assistant.io/badges/config_flow_start.svg)](https://my.home-assistant.io/redirect/config_flow_start/?domain=wyoming)

或者，你也可以手动安装 Wyoming 集成，更多信息请参阅
[Wyoming 集成文档](https://www.home-assistant.io/integrations/wyoming/)。

---

### 语音命令

查看 [可用语音命令](https://github.com/OHF-Voice/speech-to-phrase/blob/main/SENTENCES.md)

---

### 自定义语句

你可以将 \[自定义语句]\[] 添加到路径：

```
/share/speech-to-phrase/custom_sentences/<language>/sentences.yaml
```

其中 `<language>` 可选语言包括：

* `ca` - 加泰罗尼亚语
* `cs` - 捷克语
* `de` - 德语
* `el` - 希腊语
* `en` - 英语
* `es` - 西班牙语
* `eu` - 巴斯克语
* `fa` - 波斯语 / Farsi
* `fi` - 芬兰语
* `fr` - 法语
* `hi` - 印地语
* `it` - 意大利语
* `mn` - 蒙古语
* `nl` - 荷兰语
* `pl` - 波兰语
* `pt_PT` - 葡萄牙语
* `ro` - 罗马尼亚语
* `ru` - 俄语
* `sl` - 斯洛文尼亚语
* `sw` - 斯瓦希里语
* `tr` - 土耳其语

---

## 支持

有问题吗？你可以通过以下方式获得帮助：

* [Home Assistant Discord 聊天服务器][discord]
* Home Assistant [社区论坛][forum]
* 加入 Reddit 社区 [r/homeassistant][reddit]

如果发现 Bug，请在 GitHub 上 [提交 Issue][issue]。

[discord]: https://discord.gg/c5DvZ4e
[forum]: https://community.home-assistant.io
[issue]: https://github.com/home-assistant/addons/issues
[reddit]: https://reddit.com/r/homeassistant
[repository]: https://github.com/hassio-addons/repository
[sentence trigger]: https://www.home-assistant.io/docs/automation/trigger/#sentence-trigger
[exposed]: https://www.home-assistant.io/voice_control/voice_remote_expose_devices/
[custom sentences]: https://github.com/OHF-voice/speech-to-phrase?tab=readme-ov-file#custom-sentences

