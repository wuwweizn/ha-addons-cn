
# Home Assistant 插件：Samba 共享

---

## 安装

按照以下步骤在系统中安装此插件：

1. 在 Home Assistant 前端，进入 **设置** -> **插件** -> **插件商店**。
2. 找到“Samba 共享”插件并点击它。
3. 点击“安装（INSTALL）”按钮进行安装。

---

## 使用方法

1. 在配置部分设置用户名和密码。
   你可以指定任意用户名和密码；它们**与登录 Home Assistant 或电脑的账号无关**。
2. 查看已启用的共享目录。禁用你不打算使用的共享目录。需要时可以重新启用。

---

## 连接方式

* Windows 用户使用：`\\<IP_ADDRESS>\`
* MacOS 用户使用：`smb://<IP_ADDRESS>`

此插件通过 SMB（Samba）共享以下目录：

| 目录              | 描述                         |
| --------------- | -------------------------- |
| `addons`        | 本地插件目录                     |
| `addon_configs` | 插件配置文件目录                   |
| `backup`        | 备份文件目录                     |
| `config`        | Home Assistant 配置目录        |
| `media`         | 本地媒体文件目录                   |
| `share`         | 插件与 Home Assistant 共享的数据目录 |
| `ssl`           | SSL 证书目录                   |

---

## 配置

插件示例配置：

```yaml
workgroup: WORKGROUP
local_master: true
username: homeassistant
password: YOUR_PASSWORD
enabled_shares:
  - addons
  - addon_configs
  - backup
  - config
  - media
  - share
  - ssl
allow_hosts:
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16
  - 169.254.0.0/16
  - fe80::/10
  - fc00::/7
veto_files:
  - "._*"
  - ".DS_Store"
  - Thumbs.db
compatibility_mode: false
```

### 选项：`workgroup`（必填）

修改 WORKGROUP 以匹配你的网络需求。

### 选项：`local_master`（必填）

启用后插件会尝试成为子网内的本地主浏览器（local master browser）。

### 选项：`username`（必填）

用于验证 Samba 服务器的用户名。

### 选项：`password`（必填）

与用户名对应的验证密码。

### 选项：`enabled_shares`（必填）

列出可访问的 Samba 共享目录。列表中移除或注释的目录将无法访问。

### 选项：`allow_hosts`（必填）

允许访问共享文件夹的主机/网络列表。

### 选项：`veto_files`（可选）

列出不显示也不可访问的文件，用于防止客户端生成临时隐藏文件（如 macOS 的 `.DS_Store` 或 Windows 的 `Thumbs.db`）。

### 选项：`compatibility_mode`

启用此选项可在 Samba 插件中启用旧版 Samba 协议。
这可能解决某些客户端无法使用新版协议的问题，但会降低安全性。
仅在确实需要且理解可能后果时使用。

默认值：`false`

### 选项：`apple_compatibility_mode`

启用 Samba 配置以提高与 Apple 设备的兼容性。
注意，这可能在不支持 xattr 的文件系统（如 exFAT）上产生问题。

默认值：`true`

---

## 支持

有问题吗？你有多种方式获得帮助：

* [Home Assistant Discord 聊天服务器][discord]
* Home Assistant [社区论坛][forum]
* 加入 Reddit 社区 [r/homeassistant][reddit]

如果发现插件有 Bug，请在 GitHub 上 [提交 Issue][issue]。

[discord]: https://discord.gg/c5DvZ4e
[forum]: https://community.home-assistant.io
[issue]: https://github.com/home-assistant/addons/issues
[reddit]: https://reddit.com/r/homeassistant
[repository]: https://github.com/hassio-addons/repository


