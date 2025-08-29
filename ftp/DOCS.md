# Home Assistant 社区插件：FTP

FTP 协议有时仍然非常有用。虽然它比较老旧，但仍然有应用场景，例如大多数 IP 摄像头仍然支持通过 FTP 上传图片或视频。

这个插件为 Hass.io 提供了一个相对安全的 FTP 服务器。虽然 FTP 本身（未加密）并不完全安全，但此插件支持 FTP over SSL（FTPS），并将虚拟用户限制（chroot）在其主目录中。

当然，如果你愿意，也可以使用这个插件通过 FTP 访问你的 Home Assistant 配置文件。

---

## 安装

安装该插件与安装其他 Home Assistant 插件类似，非常简单。

1. 点击下面的 Home Assistant 按钮，在你的 Home Assistant 实例中打开插件。

   [![在 Home Assistant 实例中打开此插件][addon-badge]][addon]

2. 点击 **安装** 按钮安装插件。

3. 启动 **FTP** 插件。

4. 查看 **FTP** 插件的日志，确认一切正常。

---

## 配置

**注意**：*修改配置后请重启插件。*

示例配置：

```yaml
log_level: info
port: 21
data_port: 20
banner: Welcome to the Hass.io FTP service.
pasv: true
pasv_min_port: 30000
pasv_max_port: 30010
pasv_address: ""
ssl: false
certfile: fullchain.pem
keyfile: privkey.pem
implicit_ssl: false
max_clients: 5
users:
  - username: hassio
    password: changeme
    allow_chmod: true
    allow_download: true
    allow_upload: true
    allow_dirlist: true
    addons: false
    backup: true
    config: true
    media: true
    share: true
    ssl: false
  - username: camera
    password: changeme
    allow_chmod: false
    allow_download: false
    allow_upload: true
    allow_dirlist: true
    addons: false
    backup: false
    config: false
    media: false
    share: true
    ssl: false
```

**注意**：*这只是示例，请不要直接复制！请创建你自己的配置。*

---

### 选项说明

#### `log_level`

控制插件日志输出的详细程度，可根据需要调整。可选值：

* `trace`：显示每个细节，包括所有内部函数调用。
* `debug`：显示详细调试信息。
* `info`：普通（通常）事件。
* `warning`：非错误的异常事件。
* `error`：运行时错误，不需要立即处理。
* `fatal`：严重错误，插件不可用。

**注意**：每个级别会自动包含更高严重性的日志，例如 `debug` 也会显示 `info` 信息。默认值为 `info`，除非调试，否则推荐使用。
此日志级别也会影响 FTP 服务器的日志输出。

#### `port`

FTP 监听的端口。

#### `data_port`

PORT 类型连接使用的端口。

#### `banner`

FTP 服务器连接时显示的欢迎横幅文字。

#### `pasv`

是否允许 PASV 模式（被动模式）。设置为 `false` 禁用。更多信息参考 [被动与主动 FTP](https://stackoverflow.com/a/1699163/299699)。

#### `pasv_min_port` / `pasv_max_port`

PASV 模式下分配的端口范围，可用于防火墙设置。

#### `pasv_address`

覆盖 FTP 服务器在 PASV 命令中返回的 IP 地址。可以是数字 IP 或主机名（启动时解析）。留空时，使用连接的源 IP。

#### `pasv_addr_resolve`

设置为 `true`，允许主机名解析用于 PASV 连接。

#### `ssl`

启用/禁用 FTP SSL。`true` 为启用，`false` 为禁用。

#### `certfile` / `keyfile`

SSL 使用的证书和私钥文件。**注意**：必须存放在 `/ssl/` 目录下。

#### `implicit_ssl`

若为 `true`，所有连接将首先进行 SSL 握手（隐式 FTPS）。

#### `max_clients`

允许同时连接的最大客户端数量，多余客户端会收到错误。

#### `users`

指定用户列表，每个用户可以设置自己的权限：

* `username`：用户名（最多 32 个字符，只能包含 `A-Z`、`0-9`，可含 `-` 但不能开头或结尾）
* `password`：登录密码
* `allow_chmod`：允许使用 `SITE CHMOD` 命令
* `allow_download`：允许下载文件
* `allow_upload`：允许上传或修改文件（`STOR`、`DELE`、`RNFR`、`RNTO`、`MKD`、`RMD`、`APPE`、`SITE`）
* `allow_dirlist`：允许浏览有权限的目录
* `addons`：访问 `/addons`
* `backup`：访问 `/backup`
* `config`：访问 `/config`
* `media`：访问 `/media`
* `share`：访问 `/share`
* `ssl`：访问 `/ssl`

#### `i_like_to_be_pwned`

设置为 `true` 可绕过 HaveIBeenPwned 密码检查。
**注意**：强烈建议使用更强的密码，风险自负。

---

## 更新日志与版本发布

使用 [GitHub releases][releases] 记录版本变更，遵循 [语义化版本控制][semver]：

* `MAJOR`：不兼容或重大更改
* `MINOR`：向后兼容的新功能或增强
* `PATCH`：向后兼容的修复或更新

---

## 支持

如有问题，可通过以下方式获取帮助：

* [Home Assistant 社区插件 Discord](https://discord.me/hassioaddons)
* [Home Assistant Discord](https://discord.gg/c5DvZ4e)
* [Home Assistant 社区论坛](https://community.home-assistant.io/t/home-assistant-community-add-on-ftp/36799?u=frenck)
* Reddit [r/homeassistant](https://reddit.com/r/homeassistant)
* 或在 GitHub [提交 issue](https://github.com/hassio-addons/addon-ftp/issues)

---

## 作者与贡献者

原作者：[Franck Nijhof](https://github.com/frenck)
完整贡献者名单：[贡献者页面](https://github.com/hassio-addons/addon-ftp/graphs/contributors)

---

## 许可

MIT 许可证

版权 (c) 2017-2025 Franck Nijhof

允许任何人免费使用、复制、修改、发布、分发、再授权或出售软件及其文档，条件是保留版权声明和许可声明。

软件按“原样”提供，不附带任何明示或暗示的保证，包括适销性、特定用途适用性或非侵权的保证。无论在何种情况下，作者或版权持有人对任何索赔、损害或其他责任概不负责。

---

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_ftp&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[contributors]: https://github.com/hassio-addons/addon-ftp/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord]: https://discord.me/hassioaddons
[forum]: https://community.home-assistant.io/t/home-assistant-community-add-on-ftp/36799?u=frenck
[frenck]: https://github.com/frenck
[issue]: https://github.com/hassio-addons/addon-ftp/issues
[passive-vs-active]: https://stackoverflow.com/a/1699163/299699
[reddit]: https://reddit.com/r/homeassistant
[releases]: https://github.com/hassio-addons/addon-ftp/releases
[semver]: http://semver.org/spec/v2.0.0.htm
