# 配对

默认情况下，插件的 `permit_join` 设置为 `false`。要允许设备加入，需要在插件启动后激活此选项。你可以使用 [内置前端](https://www.zigbee2mqtt.io/information/frontend.html) 来完成此操作。有关如何启用内置前端的详细信息，请参阅下一节。

# 启用内置前端

启用 `ingress` 后，前端将可在你的 UI 中访问：**设置 → 插件 → Zigbee2MQTT → 在侧边栏显示**。你可以在 [Zigbee2MQTT 文档](https://www.zigbee2mqtt.io/information/frontend.html) 中找到有关该功能的更多信息。

# 配置

## 初始引导（Onboarding）

[初始引导](https://www.zigbee2mqtt.io/guide/getting-started/#onboarding) 可以让你无需手动在插件配置页面输入信息即可设置 Zigbee2MQTT。当使用全新安装启动插件（无配置时），前端会显示一个快速设置页面，让你选择各种设置，以便 Zigbee2MQTT 启动。

> \[!注意]
> 适配器的成功检测可能会因你的设置/网络环境而异。你可能需要在页面上手动输入这些 [详细信息](https://www.zigbee2mqtt.io/guide/configuration/adapter-settings.html#basic-configuration)。

> \[!提示]
> 你可以通过插件配置页面中的切换选项强制重新运行初始引导（例如更换适配器）（该选项在勾选“显示未使用的可选配置”后可见）。首次配置成功后，完成设置请务必禁用此功能。

## 手动配置

启动 Zigbee2MQTT 所需的配置可以在插件配置中完成，其余选项可通过 Zigbee2MQTT 前端进行设置。

> \[!注意]
> 通过插件配置页面设置的选项优先于 `configuration.yaml` 文件中的设置（例如，你在插件配置页面中将 `rtscts: false`，而 `configuration.yaml` 中为 `rtscts: true`，则最终会使用 `rtscts: false`）。*如果你想通过 YAML 完全控制配置，请从插件配置页面移除相关设置。*

#### 各配置节示例

* socat

  ```yaml
  enabled: false
  master: pty,raw,echo=0,link=/tmp/ttyZ2M,mode=777
  slave: tcp-listen:8485,keepalive,nodelay,reuseaddr,keepidle=1,keepintvl=1,keepcnt=5
  options: "-d -d"
  log: false
  ```
* mqtt

  ```yaml
  server: mqtt://localhost:1883
  user: my_user
  password: "my_password"
  ```
* serial

  ```yaml
  adapter: zstack
  port: /dev/serial/by-id/usb-Texas_Instruments_TI_CC2531_USB_CDC___0X00124B0018ED3DDF-if00
  ```

# 配置备份

插件会在你的数据路径中创建 `configuration.yaml` 的备份：`$DATA_PATH/configuration.yaml.bk`。升级时，应使用此备份将相关值（尤其是网络密钥）填入新配置，以避免破坏网络并重新配对所有设备。
如果在插件启动时未发现之前的备份，将会创建新的备份。

# 启用看门狗（Watchdog）

为了在出现软故障（如“适配器断开”）时自动重启 Zigbee2MQTT，可以启用看门狗。在插件配置中添加以下内容：

```yaml
watchdog: default
```

这将使用默认重试延迟：1 分钟、5 分钟、15 分钟、30 分钟、60 分钟。
也支持自定义延迟，例如：`watchdog: 5,10,30` 会使用 5 分钟、10 分钟、30 分钟的延迟。
更多信息请参阅 [文档](https://www.zigbee2mqtt.io/guide/installation/15_watchdog.html)。

# 添加新设备支持

如果你希望为 Zigbee2MQTT 添加新设备支持，请参阅 [如何支持新设备](https://www.zigbee2mqtt.io/how_tos/how_to_support_new_devices.html)。

# 注意事项

* 根据你的配置，MQTT 服务器可能需要包含端口，通常为 `1883` 或 SSL 通信的 `8883`。例如，Home Assistant 的 Mosquitto 插件可用：`mqtt://core-mosquitto:1883`。
* 要查看暴露的串口，请前往 **Supervisor → 系统 → 主机系统 → ⋮ → 硬件**。

# Socat

有些情况下，无法将串口设备转发到 Zigbee2MQTT 所在的容器中，可能是因为设备根本未物理连接到机器上。

Socat 可用于通过 TCP 将串口设备转发给 Zigbee2MQTT。更多信息请参阅 [socat 手册](https://linux.die.net/man/1/socat)。

你可以在 socat 配置节中设置以下选项：

* `enabled`：启用或禁用 socat（默认：false）
* `master`：socat 命令行中使用的主地址（必填）
* `slave`：socat 命令行中使用的从地址（必填）
* `options`：添加到 socat 命令行的额外选项（可选）
* `log`：是否将 socat 的 stdout/stderr 写入 `data_path/socat.log`（默认：false）

**注意：** 你需要根据实际情况修改 `master` 和 `slave` 选项。默认值确保 socat 监听端口 `8485` 并将输出重定向到 `/dev/ttyZ2M`。Zigbee2MQTT 的串口设置不会自动调整，需要手动修改。
