
# Home Assistant 社区插件：Plex 媒体服务器

Plex 插件将你最喜欢的媒体集中到一个地方，让你**美观且轻松地享受**它们。
本插件提供的 Plex 媒体服务器可以**整理你的个人视频、音乐和照片收藏**，并将其**流式传输到你的所有设备**。

---

## 安装

安装这个插件非常简单，与安装其他 Home Assistant 插件没有太大差别。

1. 点击下面的 Home Assistant My 按钮，在你的 Home Assistant 实例中打开此插件。

   [![在你的 Home Assistant 实例中打开此插件][addon-badge]][addon]

2. 点击“安装”按钮来安装插件。

3. 打开 [https://www.plex.tv/claim](https://www.plex.tv/claim) 获取你的 claim 令牌。

4. 在插件配置中更新你在上一步获取的 claim 代码。

5. 保存插件配置。

6. 启动“Plex 媒体服务器”插件。

7. 检查“Plex 媒体服务器”日志，确认一切正常。

8. 登录 Plex 管理界面并完成设置流程。

**注意**：添加媒体位置时，请使用 `/share` 和 `/media` 作为基目录。

---

## 配置

**注意**：*配置更改后请记得重启插件。*

示例插件配置：

```yaml
log_level: info
claim_code: claim-cAMrqFrenckFU4x445Tn
```

**注意**：*这只是示例，请不要直接复制！请创建你自己的配置！*

### 选项：`log_level`

`log_level` 选项控制插件的日志输出级别，可根据需要设置详细或简略，这在排查未知问题时非常有用。可选值如下：

* `trace`：显示每一个细节，如所有内部函数调用。
* `debug`：显示详细调试信息。
* `info`：普通（通常）有趣的事件。
* `warning`：非错误的异常情况。
* `error`：运行时错误，不需要立即处理。
* `fatal`：发生严重错误，插件无法使用。

请注意，每个级别会自动包含更严重级别的日志消息，例如 `debug` 也会显示 `info` 消息。
默认 `log_level` 为 `info`，除非排查问题，否则推荐使用此设置。

### 选项：`claim_code`

为了让你的服务器登录到 Plex 账户，需要一个“Claim Code”。
登录 Plex 使 Plex 可以定位并连接到你的服务器，同时解锁各种功能。

获取代码请访问 [https://www.plex.tv/claim](https://www.plex.tv/claim)。

此代码在插件中仅使用一次。服务器成功认证后，可以删除该代码。

---

## 解决 Plex 连接问题

Plex 设置简单，大部分配置会自动检测。但有时它无法识别家庭网络中的 IP，这可能导致部分 Plex 应用（如 Samsung Tizen Plex 应用）连接失败。

这不是 Plex 的问题，而是由于插件运行在 Docker 环境中造成的。幸运的是，Plex 提供了一个隐藏选项可解决此问题：

* 登录 Plex 网页界面。
* 进入设置。
* 点击服务器标签页。
* 左侧选择“网络”。
* 确保使用高级视图（右上角有“显示高级”按钮）。
* 在“自定义服务器访问 URL”字段中添加你的自定义 URL。

自定义 URL 是 Plex 客户端尝试连接 Plex 时使用的额外 URL，可列出多个，用逗号分隔。

示例：

```txt
http://hassio.local:32400,http://192.168.1.88:32400,http://mydomain.duckdns.org:32400
```

---

## 已知问题和限制

* 此插件支持 ARM 设备，但至少需为 ARMv7 设备（Raspberry Pi 1 和 Zero 不支持）。
* 此插件可在 Raspberry Pi 上运行，但性能有限，可能无法流畅播放媒体，不建议在此类设备上使用。
* 插件无法为你添加或挂载额外的 USB 或其他设备，这是 Home Assistant 的限制。如需使用额外设备，必须自行修改宿主系统，此操作不受 Home Assistant 或社区插件团队支持。
* Plex Pass 用户可访问 Beta 版本的新功能，而本插件暂不支持运行 Beta 版本。
* 插件不支持通过 DLNA 使用 Plex。

---

## 更新日志与版本发布

本仓库使用 [GitHub Releases][releases] 功能记录更新日志。

版本遵循 [语义化版本控制][semver]，格式为 `MAJOR.MINOR.PATCH`。
版本号增量规则如下：

* `MAJOR`：不兼容或重大变更。
* `MINOR`：向后兼容的新功能或增强。
* `PATCH`：向后兼容的错误修复或包更新。

---

## 支持

有问题吗？你有多种方式获得帮助：

* [Home Assistant 社区插件 Discord 聊天][discord]，用于插件支持和功能请求。
* [Home Assistant Discord 聊天服务器][discord-ha]，用于一般讨论和问题。
* Home Assistant [社区论坛][forum]。
* 加入 Reddit 社区 [r/homeassistant][reddit]。

你也可以在 GitHub [这里打开 issue][issue]。

---

## 作者与贡献者

本仓库最初由 [Franck Nijhof][frenck] 搭建。

完整作者与贡献者名单，请查看 [贡献者页面][contributors]。

---

## 许可证

MIT 许可证

版权所有 (c) 2018-2025 Franck Nijhof

特此免费授予任何获得本软件及相关文档文件（“软件”）副本的人无限制使用权，包括但不限于使用、复制、修改、合并、发布、分发、再授权及/或销售本软件的副本，并允许向其提供软件的人在符合以下条件下使用本软件：

上述版权声明和本许可声明必须包含在软件的所有副本或重要部分中。

本软件按“原样”提供，不附带任何明示或暗示的保证，包括但不限于适销性、适用性或非侵权性。
作者或版权持有人不对因使用本软件而产生的任何索赔、损害或其他责任承担责任，无论是在合同、侵权或其他情况下。

---

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_plex&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[contributors]: https://github.com/hassio-addons/addon-plex/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord]: https://discord.me/hassioaddons
[forum]: https://community.home-assistant.io/t/home-assistant-community-add-on-plex-media-server/54383?u=frenck
[frenck]: https://github.com/frenck
[issue]: https://github.com/hassio-addons/addon-plex/issues
[reddit]: https://reddit.com/r/homeassistant
[releases]: https://github.com/hassio-addons/addon-plex/releases
[semver]: https://semver.org/spec/v2.0.0.html


