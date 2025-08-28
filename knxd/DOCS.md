
# Home Assistant 社区插件：KNXD

## 安装

按照以下步骤在系统中安装该插件：

1. 在 Home Assistant 前端进入 **Supervisor（监督者）** -> **Add-on Store（插件商店）**。
2. 如果你还没有将此插件仓库添加到 Supervisor，请点击右上角菜单图标，选择 **Repositories（仓库）**，添加 `https://github.com/da-anda/hass-io-addons` 作为新的仓库，然后关闭对话框。
3. 找到 **“KNXD”** 插件并点击它。
4. 点击 **“INSTALL（安装）”** 按钮。

## 配置

插件配置示例：

```yaml
    "address": "0.0.1",
    "client_address": "0.0.2:8",
    "interface": "tpuart",
    "device": "/dev/ttyACM0",
    "usb_filters": "",
    "custom_config": ""
```

### 选项说明

这些选项的部分描述来自 `knxd` 的[官方文档](https://github.com/knxd/knxd/blob/master/doc/inifile.rst)。你可以在那里找到更多示例和详细说明。

#### 选项 `address`

KNXD 守护进程自身的 KNX 地址。用于例如组缓存发出的请求。

#### 选项 `client_address`

分配给客户端连接的地址范围。注意，其中的长度参数表示要分配的地址数量。

示例： `1.2.3:5` （这会将地址 `1.2.3` 到 `1.2.7` 分配给 KNXD 的客户端。）

#### 选项 `interface`

`knxd` 用于与 KNX 总线通信的驱动。对于此插件的常见使用场景，最常见的有：

* `tpuart` （适用于基于 UART 的 KNX 接口，例如 Busware.de 提供的硬件）
* `usb` （适用于商用 KNX USB 接口）

完整的驱动选项列表可参考 `knxd` 文档中的[驱动章节](https://github.com/knxd/knxd/blob/master/doc/inifile.rst#drivers)。

#### 选项 `device` （某些接口可选）

在 Linux 中你的适配器的物理设备地址。例如：

* **TPUART 接口**: `/dev/ttyACM0`
* **USB 接口**: 可以尝试留空，让 `knxd` 自动检测设备。如果留空无效，可以手动指定设备地址，例如 `/dev/ttyAMA0`。

请注意，这里的地址只是示例，你的设备可能不同。要找到实际设备地址，你需要通过 SSH 登录到主机操作系统（**不是 Supervisor 容器！**），然后检查连接的设备。

#### 选项 `usb_filters` （可选）

当使用 USB 接口时，可以指定额外的过滤器。详细说明可参考官方 `knxd` 文档中的[过滤器章节](https://github.com/knxd/knxd/blob/master/doc/inifile.rst#filters)。

#### 选项 `custom_config` （已弃用）

允许你编写自定义的 `knxd` ini 配置，替代此插件提供的模板。

当你启用自定义配置时，插件默认提供的配置会被替换，其他所有上面提到的配置选项都会被忽略。具体可参考 [knxd 文档](https://github.com/knxd/knxd/blob/master/doc/inifile.rst)。

请注意：自插件版本 **0.6.0** 起，此配置选项已被弃用，并将在未来更新中移除。现在你可以在插件对应的 `addon_config` 目录中提供自定义 ini 配置文件。如果你安装了 **SMB 共享插件**，则可以通过网络共享方式访问该目录。

## 支持

如有任何问题，可以加入 HomeAssistant 社区，在[插件讨论贴](https://community.home-assistant.io/t/knxd-add-on-covert-your-knx-usb-interface-into-an-ip-interface-that-can-be-used-by-ha/38108/38)中提问。

如果你发现了 bug，请到 [Github](https://github.com/da-anda/hass-io-addons/issues) 提交工单。


