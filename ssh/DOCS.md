
# Home Assistant 插件：终端 & SSH（Terminal & SSH）

---

## 安装

按照以下步骤在系统中安装此插件：

1. 此插件仅对“高级模式”用户可见。要启用高级模式，请进入 **个人资料** -> 打开 **高级模式**。
2. 在 Home Assistant 前端，进入 **设置** -> **插件** -> **插件商店**。
3. 找到“终端 & SSH（Terminal & SSH）”插件并点击它。
4. 点击“安装（INSTALL）”按钮。

---

## 使用方法

此插件为 Home Assistant 添加了两个主要功能：

* 一个可在浏览器中使用的 Web 终端
* 允许使用 SSH 客户端连接到你的系统

无论你使用 Web 终端还是 SSH 客户端连接，你最终都进入这个插件的容器中。Home Assistant 配置目录位于 `/config` 路径下。

此插件自带 [Home Assistant CLI](https://www.home-assistant.io/common-tasks/os#home-assistant-via-the-command-line)，可使用以下命令尝试：

```bash
ha help
```

---

### Web 终端

你可以通过点击插件信息页上的“打开 Web UI（Open Web UI）”按钮访问 Web 终端。
如果在信息页将“在侧边栏显示（Show in sidebar）”设置为“开启”，侧边栏将添加一个快捷入口，可快速访问 Web 终端。

从 Web UI 复制文本：

1. 按住 SHIFT 键。
2. 使用鼠标选择要复制的文本。
3. 松开鼠标左键后，文本会被复制到系统剪贴板。

向 Web UI 粘贴文本：

1. 按 SHIFT + INSERT。

---

### SSH 服务器连接

网络上的远程 SSH 默认是关闭的（见网络配置部分）。
要使用 SSH 客户端（如 PuTTY 或 Linux 终端）连接，需要为此插件提供额外配置以启用 SSH：

* 提供认证凭据——密码或 SSH 密钥
* 指定要绑定的 TCP 端口（在 Home Assistant 主机上）

然后可以使用用户名 `root` 连接到指定端口。
请注意，启用 SSH 服务器可能会降低 Home Assistant 系统的安全性，因为这可能允许互联网用户尝试访问你的系统。系统安全性还取决于网络设置、路由器配置、防火墙使用等。通常建议：除非完全理解其影响，否则不要启用此功能。

如果使用 SSH 客户端连接，强烈建议使用公钥/私钥登录。只要你保管好私钥，系统就更难被入侵。相比之下，使用密码通常安全性较低。
生成 SSH 公钥/私钥的方法，请参阅 [Windows 指南][keygen-windows] 或 [其他平台指南][keygen]。

**注意**：按照上面指南生成密钥时，请选择 ECDSA 类型而非 RSA，RSA 已不再受支持。

通过密码登录会禁用基于密钥的登录，二者不能同时使用。

---

## 配置

插件配置示例：

```yaml
authorized_keys:
  - "ssh-rsa AKDJD3839...== my-key"
password: ''
apks: []
server:
  tcp_forwarding: false
```

### 选项：`apks`

要在插件容器中安装的额外软件包列表。

### 选项：`authorized_keys`

你希望用于登录的 **公钥**。可添加多个公钥。
如果添加密钥时报错，可能是因为公钥中含有 YAML 语法特殊字符。可用双引号将密钥括起来。

### 选项：`password`

设置登录密码。**不推荐使用此方式**。

### 选项组：`server`

一些 SSH 服务器相关选项。

#### 选项：`tcp_forwarding`

是否允许 TCP 端口转发（如 -L、-R 等）。

**注意**：启用此选项会降低 SSH 服务器安全性，但这个警告有一定争议。

---

## 网络

此部分仅在你希望通过 SSH 客户端（如 PuTTY 或 Linux 终端）连接 Home Assistant 时才相关。
在网络配置中指定 SSH TCP 服务器端口，插件会将主机端口映射到“终端 & SSH”插件容器中。
SSH 默认端口为 `22`。

远程 SSH 可通过清空端口输入框、保存配置并重启插件再次禁用。

---

## 已知问题与限制

* 此插件无法以 root 身份安装软件包或执行任意操作，这是 Home Assistant 的限制。

---

## 支持

有问题吗？可通过以下方式获取帮助：

* [Home Assistant Discord 聊天服务器][discord]
* Home Assistant [社区论坛][forum]
* Reddit 社区 [r/homeassistant][reddit]

如发现 Bug，请在 GitHub 上 [提交 Issue][issue]。

[discord]: https://discord.gg/c5DvZ4e
[forum]: https://community.home-assistant.io
[issue]: https://github.com/home-assistant/addons/issues
[keygen-windows]: https://www.digitalocean.com/community/tutorials/how-to-create-ssh-keys-with-putty-to-connect-to-a-vps
[keygen]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
[reddit]: https://reddit.com/r/homeassistant


