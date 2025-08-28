# Home Assistant 社区插件：phpMyAdmin

phpMyAdmin 是一个用于 MySQL 和 MariaDB 的数据库管理工具。你可以通过用户界面执行常用操作（管理数据库、表、列、关系、索引、用户、权限等），同时仍可以直接执行任何 SQL 语句。

此插件专为管理官方 Home Assistant MariaDB 插件而设计。

## 安装

安装此插件与安装其他 Home Assistant 插件方法相同，非常简单。

1. 点击下面的 Home Assistant 按钮，在你的 Home Assistant 实例中打开该插件。

   [![在你的 Home Assistant 实例中打开此插件][addon-badge]][addon]

2. 点击 “安装” 按钮安装插件。

3. 启动 “phpMyAdmin” 插件。

4. 开始使用插件！

## 配置

**注意**：*更改配置后，请记得重启插件。*

示例插件配置：

```yaml
log_level: info
```

**注意**：*这只是示例，请不要直接复制粘贴！请根据实际情况创建你自己的配置。*

### 选项：`upload_limit`

默认上传大小限制（用于导入等操作）为 64MB。可以通过此选项增加，例如设置 `100` 表示 100MB。

### 选项：`log_level`

`log_level` 控制插件的日志输出级别，可根据需求调节详细程度，有助于排查问题。可能值：

* `trace`：显示所有细节，包括所有内部调用函数。
* `debug`：显示详细调试信息。
* `info`：普通（通常）重要事件。
* `warning`：异常情况，但不是错误。
* `error`：运行时错误，无需立即处理。
* `fatal`：严重错误，插件不可用。

请注意，每个级别自动包含更高严重性级别的日志信息，例如 `debug` 也会显示 `info` 消息。默认 `log_level` 为 `info`，除非排查问题，否则推荐使用此设置。

## 已知问题与限制

* 此插件需要 core MariaDB 插件版本 2.0 或更高。
* 此插件仅用于管理官方 Home Assistant MariaDB 插件，不能连接其他 MySQL 或 MariaDB 服务器。

## 更新日志与版本发布

本仓库使用 [GitHub releases][releases] 功能记录更新日志。

版本遵循 [语义化版本][semver]，格式为 `MAJOR.MINOR.PATCH`。版本更新规则如下：

* `MAJOR`：不兼容或重大更改。
* `MINOR`：向后兼容的新功能或增强。
* `PATCH`：向后兼容的错误修复和包更新。

## 支持

有问题吗？你有多种方式获取帮助：

* [Home Assistant 社区插件 Discord 聊天服务器][discord]，用于插件支持和功能请求。
* Home Assistant [Discord 聊天服务器][discord-ha]，用于一般讨论和问题。
* Home Assistant [社区论坛][forum]。
* Reddit [/r/homeassistant][reddit] 讨论区。

如果发现 bug，请在 GitHub 上 [提交 issue][issue]。

## 作者与贡献者

此仓库的最初创建者为 [Franck Nijhof][frenck]。

完整作者与贡献者列表，请查看 [贡献者页面][contributors]。

## 许可

MIT 许可证

版权所有 (c) 2021-2025 Franck Nijhof

特此免费授予任何获得本软件及相关文档文件（“软件”）副本的人无限制权利，包括但不限于使用、复制、修改、合并、发布、分发、再许可及/或销售软件副本，并允许向其提供软件的人这样做，遵守以下条件：

上述版权声明和本许可声明必须包含在软件的所有副本或主要部分中。

本软件按“原样”提供，不附带任何形式的明示或暗示担保，包括但不限于适销性、特定用途适用性及非侵权的保证。在任何情况下，作者或版权持有人均不对因软件或软件使用或其他交易引起的任何索赔、损害或其他责任承担责任。

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_phpmyadmin&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[contributors]: https://github.com/hassio-addons/addon-phpmyadmin/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord]: https://discord.me/hassioaddons
[forum]: https://community.home-assistant.io/t/home-assistant-community-add-on-phpmyadmin/171729?u=frenck
[frenck]: https://github.com/frenck
[issue]: https://github.com/hassio-addons/addon-phpmyadmin/issues
[reddit]: https://reddit.com/r/homeassistant
[releases]: https://github.com/hassio-addons/addon-phpmyadmin/releases
[semver]: https://semver.org/spec/v2.0.0.html
