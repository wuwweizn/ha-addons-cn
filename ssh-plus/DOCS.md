
# Home Assistant 社区插件：高级 SSH & Web 终端

此插件允许你通过 SSH 或 Web 终端登录 Home Assistant 实例，访问系统文件夹，同时提供命令行工具用于重启、更新和检查实例。

这是 Home Assistant 官方提供的 \[SSH 插件]\[hass-ssh] 的增强版本，重点在于安全性、可用性和灵活性，同时提供 Web 界面访问。

---

## ⚠️ 警告

高级 SSH & Web 终端插件非常强大，可访问系统的几乎所有工具和硬件。

虽然该插件在开发和维护过程中注重安全，但如果交给不熟悉的人或操作不当，可能会损坏系统。

---

## 功能

此插件提供 SSH 服务器（基于 \[OpenSSH]\[openssh]）以及 Web 终端（可集成在 Home Assistant 前端）。
此外，还包含以下功能：

* 直接在 Home Assistant 前端访问命令行！
* SSH 的安全默认配置：

  * 仅允许配置的用户登录，即使创建了多个用户。
  * 仅使用已知的安全加密算法。
  * 限制登录尝试次数，提高对暴力破解的防护。
* 提供 SSH 兼容模式，以支持旧客户端连接。
* 支持 Mosh，可在移动或网络不稳定时保持连接。
* 默认禁用 SFTP，可根据需要启用。
* 如果 Home Assistant 是通过通用 Linux 安装程序安装，也兼容。
* 用户名可自定义，不再必须使用 `root`。
* 自定义 SSH 客户端设置和密钥可在插件重启后保持。
* 日志级别设置，可帮助排查问题。
* 可访问音频、UART/串口设备及 GPIO 引脚。
* 提升权限，允许调试和测试更多情况。
* 可访问主机系统的 dbus。
* 可选择访问主机上运行的 Docker 实例。
* 使用主机网络，可开放端口或运行小型守护进程。
* 可在启动时安装自定义 Alpine 包，每次登录都可使用。
* 可在插件启动时执行自定义命令，定制你的 shell 环境。
* 默认使用 \[ZSH]\[zsh] 作为 shell，适合初学者和高级用户。预装了 \["Oh My ZSH"]\[ohmyzsh] 并启用了一些插件。
* 自带常用工具：curl、wget、rsync、git、nmap、Mosquitto 客户端、MariaDB/MySQL 客户端、Wake-on-LAN、nano、vim、tmux 及常用网络工具。

---

## 安装

安装方式与其他 Home Assistant 插件类似：

1. 点击下方 Home Assistant 按钮，在你的实例中打开插件。

   [![在 Home Assistant 中打开此插件][addon-badge]][addon]

2. 点击“安装（Install）”按钮。

3. 配置 `username` 和 `password` / `authorized_keys` 选项。

4. 启动“高级 SSH & Web 终端”插件。

5. 查看插件日志，确保一切正常。

---

## 配置

**注意**：更改配置后，请重启插件。

SSH 插件配置示例：

```yaml
log_level: info
ssh:
  username: homeassistant
  password: ""
  authorized_keys:
    - ssh-ed25519 AASDJKJKJFWJFAFLCNALCMLAK234234.....
  sftp: false
  compatibility_mode: false
  allow_agent_forwarding: false
  allow_remote_port_forwarding: false
  allow_tcp_forwarding: false
zsh: true
share_sessions: true
packages:
  - build-base
init_commands:
  - ls -la
```

**注意**：此示例仅作参考，请根据实际需求创建自己的配置。

---

### 选项：`log_level`

控制插件日志输出级别，可根据需要设置更详细或简略。可选值：

* `trace`：显示所有细节，包括所有内部函数调用。
* `debug`：显示详细调试信息。
* `info`：正常信息（默认，一般情况下足够）。
* `warning`：非错误的异常事件。
* `error`：运行时错误，不需立即处理。
* `fatal`：严重错误，插件无法使用。

每个级别会自动包含更严重级别的日志，例如 `debug` 会包含 `info` 日志。默认推荐 `info`，调试时可使用 `debug` 或 `trace`。

⚠️ 使用 `trace` 或 `debug` 会让 SSH 和终端守护进程进入调试模式，此时 SSH 仅允许单个连接。

---

### SSH 配置组：`ssh`

以下选项仅适用于 SSH 守护进程。

#### `username`

设置通过 SSH 登录时使用的用户名。认证通过后，你将以 `root` 用户身份登录。

* 建议不要使用 `root` 作为用户名。
* 用户名会自动转为小写。
* **注意**：如果要启用 SFTP，必须设置为 `root`。

#### `password`

设置登录密码。留空则禁用密码登录。
**不推荐使用密码登录**。

#### `authorized_keys`

添加一个或多个公钥，用于 SSH 登录。推荐使用密钥登录而非密码。
请确保以列表形式写入 YAML 中（`[]` 逗号分隔）。
可参考 \[GitHub SSH 文档]\[github-ssh] 学习公钥/私钥使用方法。

#### `sftp`

是否启用 SFTP 支持。仅在需要时启用。
⚠️ 启用 SFTP 时，必须将用户名设为 `root`。

#### `compatibility_mode`

允许旧客户端使用默认加密方法连接。
⚠️ 启用后会降低 SSH 安全性。

#### `allow_agent_forwarding`

是否允许 SSH agent 转发。
⚠️ 启用后可能降低 SSH 安全性。

#### `allow_remote_port_forwarding`

是否允许远程主机访问客户端转发的端口。
⚠️ 启用后需谨慎操作。

#### `allow_tcp_forwarding`

是否允许 TCP 转发。
⚠️ 启用后可能降低 SSH 安全性。

---

### 共享设置（SSH + Web 终端）

#### `zsh`

默认使用 ZSH 作为 shell。设为 `false` 可切换回 Bash。

#### `share_sessions`

默认情况下，Web 终端与 SSH 的会话共享。
设为 `false` 可禁用此行为，使 SSH 恢复传统行为。

#### `packages`

可指定额外的 [Alpine 软件包][alpine-packages]（如 Python、Joe、Irssi）在 shell 环境中安装。
⚠️ 安装过多包会延长插件启动时间。

#### `init_commands`

启动插件时执行自定义命令，可每次启动自动执行列表中的命令。

---

## 已知问题与限制

* 启用 SFTP 时，用户名必须设为 `root`。
* 使用 rsync 进行文件传输时，用户名必须设为 `root`。

---

## 更新日志 & 发布版本

本仓库使用 \[GitHub Release]\[releases] 管理更新日志。

版本遵循 \[语义化版本号]\[semver] 格式：`MAJOR.MINOR.PATCH`

* `MAJOR`：不兼容或重大改动
* `MINOR`：向后兼容的新功能或增强
* `PATCH`：向后兼容的 Bug 修复或包更新

---

## 支持

遇到问题可通过以下方式获取帮助：

* \[Home Assistant 社区插件 Discord]\[discord]（插件支持与功能请求）
* \[Home Assistant Discord]\[discord-ha]（常规 Home Assistant 讨论）
* Home Assistant \[社区论坛]\[forum]
* Reddit 社区 \[r/homeassistant]\[reddit]
* 或在 GitHub \[提交 Issue]\[issue]

---

## 作者与贡献者

此仓库最初由 \[Franck Nijhof]\[frenck] 创建。
完整贡献者列表见 [Contributors 页面][contributors]。

---

## 许可协议

MIT License

版权所有 (c) 2017-2025 Franck Nijhof

授权任何人免费使用、复制、修改、合并、发布、分发、再许可或销售本软件及文档，条件是保留上述版权声明和许可声明。

软件按“原样”提供，不附带任何明示或暗示的保证，包括适销性、特定用途适用性或非侵权保证。作者或版权持有人不承担任何因使用本软件而产生的责任。

---

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_ssh&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[alpine-packages]: https://pkgs.alpinelinux.org/packages
[contributors]: https://github.com/hassio-addons/addon-ssh/graphs/contributors
