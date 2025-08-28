
# Home Assistant 插件：MariaDB

## 安装

按照以下步骤在系统中安装此插件：

1. 在 Home Assistant 前端导航到 **设置** -> **插件** -> **插件商店**。
2. 找到 **MariaDB** 插件并点击进入。
3. 点击 **安装** 按钮。

## 使用方法

1. 在 `logins` -> `password` 字段中设置一个强壮且唯一的密码。
2. 启动插件。
3. 检查插件日志输出以查看结果。
4. 在 Home Assistant 配置中添加 `recorder` 集成。

## 插件配置

MariaDB 服务器插件可以根据你的需求进行调整。本节描述了插件的每个配置选项。

插件配置示例：

```yaml
databases:
  - homeassistant
logins:
  - username: homeassistant
    password: PASSWORD
  - username: read_only_user
    password: PASSWORD
rights:
  - username: homeassistant
    database: homeassistant
  - username: read_only_user
    database: homeassistant
    privileges:
      - SELECT
```

### 选项: `databases` （必填）

数据库名称，例如 `homeassistant`。支持多个数据库。

### 选项: `logins` （必填）

该部分定义了在 MariaDB 中创建的用户。[Create User 文档][createuser]。

### 选项: `logins.username` （必填）

数据库用户名，例如 `homeassistant`。[用户名文档][username]。

### 选项: `logins.password` （必填）

数据库用户密码，应设置为强壮且唯一的密码。

### 选项: `rights` （必填）

该部分定义了在 MariaDB 中授予用户的权限。[GRANT 文档][grant]。

### 选项: `rights.username` （必填）

应与 `logins` -> `username` 中定义的用户名一致。

### 选项: `rights.database` （必填）

应与 `databases` 中定义的数据库名一致。

### 选项: `rights.privileges` （可选）

授予用户的权限列表，来自 [GRANT 文档][grant]，例如 `SELECT` 和 `CREATE`。
如果省略，将授予用户 **所有权限 (ALL PRIVILEGES)**。
不建议限制 Home Assistant 使用的用户权限，但如果你希望其他应用只能查看 recorder 数据，可以创建一个只读用户。

### 选项: `mariadb_server_args` （可选）

部分用户在大型数据库上更新 Home Assistant 模式时遇到过 [错误][migration-issues]。
如果系统内存充足，可以定义推荐参数来避免问题。

示例：`--innodb_buffer_pool_size=512M`

## Home Assistant 配置

MariaDB 将被 Home Assistant 中的 `recorder` 和 `history` 组件使用。
更多配置方法请参考 [recorder 集成文档][mariadb-ha-recorder]。

Home Assistant 配置示例：

```yaml
recorder:
  db_url: mysql://homeassistant:password@core-mariadb/homeassistant?charset=utf8mb4
```

## 支持

有问题？可以通过以下方式获取帮助：

* 加入 [Home Assistant Discord 聊天服务器][discord]。
* 访问 Home Assistant [社区论坛][forum]。
* 加入 [Reddit 子版块][reddit]：[/r/homeassistant][reddit]。

如果你发现了 bug，请 [在 GitHub 上提交 issue][issue]。

---

[createuser]: https://mariadb.com/kb/en/create-user/
[username]: https://mariadb.com/kb/en/create-user/#user-name-component
[hostname]: https://mariadb.com/kb/en/create-user/#host-name-component
[grant]: https://mariadb.com/kb/en/grant/
[migration-issues]: https://github.com/home-assistant/core/issues/125339
[mariadb-ha-recorder]: https://www.home-assistant.io/integrations/recorder/
[discord]: https://discord.gg/c5DvZ4e
[forum]: https://community.home-assistant.io
[i386-shield]: https://img.shields.io/badge/i386-yes-green.svg
[issue]: https://github.com/home-assistant/addons/issues
[reddit]: https://reddit.com/r/homeassistant
[repository]: https://github.com/hassio-addons/repository


