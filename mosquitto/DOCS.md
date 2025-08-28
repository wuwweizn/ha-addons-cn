# Home Assistant 插件：Mosquitto broker

## 安装

按照以下步骤在系统中安装该插件：

1. 在 Home Assistant 前端进入 **设置** -> **插件** -> **插件商店**。
2. 找到 **Mosquitto broker** 插件并点击它。
3. 点击 **安装** 按钮。

## 使用方法

该插件提供了一些可用选项。要启动插件：

1. 启动插件。
2. 耐心等待几分钟。
3. 查看插件日志输出以确认结果。

在 Home Assistant 前端中为 MQTT 创建一个新用户：
进入 **设置** -> **人员** -> **用户** （而不是 Mosquitto 的 **配置** 选项卡）。

注意事项：

1. 用户名不能是 `homeassistant` 或 `addons`，这两个是保留用户名。
2. 如果看不到创建新用户的选项，请确保在 Home Assistant 个人资料中启用了 **高级模式**。

要使用 Mosquitto 作为 broker，前往集成页面，一键安装配置：

1. 在 Home Assistant 前端进入 **设置** -> **设备与服务** -> **集成**。
2. 页面顶部应会自动发现 MQTT 作为一个集成。
3. 选择它，并勾选启用 MQTT 自动发现（可选），然后点击提交。

如果之前有旧的 MQTT 设置，请移除旧的集成并重启 Home Assistant 才能看到新的集成。

## 配置

插件配置示例：

```yaml
logins: []
customize:
  active: false
  folder: mosquitto
certfile: fullchain.pem
keyfile: privkey.pem
require_certificate: false
```

### 选项：`logins`（可选）

创建本地用户（用户名+密码）。
通常不需要，因为你可以直接使用 Home Assistant 用户系统，无需额外配置。
如果确实想创建本地用户，可以这样写：

```yaml
logins:
  - username: user
    password: passwd
```

你也可以选择设置一个经过哈希处理的密码（使用容器内的 `pw` 命令生成）：

```console
$ pw -p "foo"
PBKDF2$sha512$100000$qsU7xQ8YCV/9nRuBBJVTxA==$jqw94Ej3aEr97UofY6rClmVCRkTdDiubQW0A6ZYmUI+pZjW9Hax+2w2FeYB3y5ut1SliB7+HAwIl2iONLKkohw==
```

```yaml
logins:
  - username: user
    password: "PBKDF2$sha512$100000$qsU7xQ8YCV/9nRuBBJVTxA==$jqw94Ej3aEr97UofY6rClmVCRkTdDiubQW0A6ZYmUI+pZjW9Hax+2w2FeYB3y5ut1SliB7+HAwIl2iONLKkohw=="
    password_pre_hashed: true
```

**注意**：该插件不支持匿名登录，所有连接必须使用用户名/密码。`allow_anonymous true` 和匿名 ACL 都无法使用。

#### 选项：`customize.active`

如果设为 `true`，将会读取额外的配置文件。

默认值：`false`

#### 选项：`customize.folder`

指定额外配置文件（`*.conf`）所在的文件夹。

### 选项：`cafile`（可选）

包含根证书的文件，需放在 Home Assistant 的 `ssl` 文件夹中。

### 选项：`certfile`

包含证书及其链的文件，需放在 `ssl` 文件夹中。

### 选项：`keyfile`

包含私钥的文件，需放在 `ssl` 文件夹中。

**关于 `certfile` 和 `keyfile`**

* 如果未提供：

  * 可使用非加密连接（默认端口 `1883`，websocket 为 `1884`）
* 如果提供：

  * 仍可使用非加密连接（`1883`，`1884`）
  * 也可使用加密连接（`8883`，websocket 为 `8884`），但客户端必须信任服务器证书

### 选项：`require_certificate`

* 如果设为 `false`：

  * 客户端 **不需要** 提供证书，用户名/密码即可
  * 忽略 `cafile` 选项

* 如果设为 `true`：

  * 客户端 **必须** 提供证书，用户名/密码不足以连接
  * 必须提供 CA 根证书 (`cafile`)
  * 客户端证书必须由提供的 CA 签发

### 选项：`debug`

设为 `true` 可开启 mosquitto 和认证插件的调试日志（可能会泄露敏感信息，不建议长期开启）。

## Home Assistant 用户管理

该插件绑定到 Home Assistant 用户系统，因此 MQTT 客户端可使用这些凭据。
也可以在插件配置中额外设置本地用户。
内部保留了 `homeassistant` 和 `addons` 两个用户，不能重复使用。

## 禁用不安全端口（1883/1884）

在插件页面的网络设置卡片中删除这些端口（设为空）即可禁用。

### 访问控制列表（ACLs）

可以根据用户限制其访问的主题。推荐为每个客户端创建单独的用户并设置对应 ACL。

示例：为 `[YOUR_MQTT_USER]` 启用 **不受限访问**。

1. 启用自定义配置：

```yaml
customize:
  active: true
  folder: mosquitto
```

2. 创建 `/share/mosquitto/acl.conf` 文件，内容为：

```text
acl_file /share/mosquitto/accesscontrollist
```

3. 创建 `/share/mosquitto/accesscontrollist` 文件，内容为：

```text
user addons
topic readwrite #

user homeassistant
topic readwrite #

user [YOUR_MQTT_USER]
topic readwrite #
```

`/share` 文件夹可通过 SMB 访问，或在主机文件系统中 `/usr/share/hassio/share` 访问。

## 支持

有问题？可以通过以下渠道寻求帮助：

* [Home Assistant Discord 聊天服务器][discord]
* [Home Assistant 社区论坛][forum]
* [Reddit 子版块][reddit]：[/r/homeassistant][reddit]

如果发现了 bug，请在 [GitHub 提交 issue][issue]。

[discord]: https://discord.gg/c5DvZ4e
[forum]: https://community.home-assistant.io
[issue]: https://github.com/home-assistant/addons/issues
[reddit]: https://reddit.com/r/homeassistant
[repository]: https://github.com/hassio-addons/repository
[mosquitto]: https://mosquitto.org/


