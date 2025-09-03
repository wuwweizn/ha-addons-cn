# Home Assistant 插件：Emby

[![捐赠][donation-badge]](https://www.buymeacoffee.com/alexbelgium)
[![捐赠][paypal-badge]](https://www.paypal.com/donate/?hosted_button_id=DZFULJZTP3UQA)

![版本](https://img.shields.io/badge/dynamic/json?label=Version\&query=%24.version\&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Femby%2Fconfig.json)
![Ingress](https://img.shields.io/badge/dynamic/json?label=Ingress\&query=%24.ingress\&durl=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Femby%2Fconfig.json)
![架构](https://img.shields.io/badge/dynamic/json?color=success\&label=Arch\&query=%24.arch\&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Femby%2Fconfig.json)

[![Codacy Badge](https://app.codacy.com/project/badge/Grade/9c6cf10bdbba45ecb202d7f579b5be0e)](https://www.codacy.com/gh/alexbelgium/hassio-addons/dashboard?utm_source=github.com&utm_medium=referral&utm_content=alexbelgium/hassio-addons&utm_campaign=Badge_Grade)
[![GitHub Super-Linter](https://img.shields.io/github/actions/workflow/status/alexbelgium/hassio-addons/weekly-supelinter.yaml?label=Lint%20code%20base)](https://github.com/alexbelgium/hassio-addons/actions/workflows/weekly-supelinter.yaml)
[![Builder](https://img.shields.io/github/actions/workflow/status/alexbelgium/hassio-addons/onpush_builder.yaml?label=Builder)](https://github.com/alexbelgium/hassio-addons/actions/workflows/onpush_builder.yaml)

[donation-badge]: https://img.shields.io/badge/Buy%20me%20a%20coffee%20\(no%20paypal\)-%23d32f2f?logo=buy-me-a-coffee&style=flat&logoColor=white
[paypal-badge]: https://img.shields.io/badge/Buy%20me%20a%20coffee%20with%20Paypal-0070BA?logo=paypal&style=flat&logoColor=white

*感谢所有给我的仓库点星标的朋友！点击下面的图片即可 star，本项目就会显示在右上角，谢谢！*

[![Stargazers repo roster for @alexbelgium/hassio-addons](https://raw.githubusercontent.com/alexbelgium/hassio-addons/master/.github/stars2.svg)](https://github.com/alexbelgium/hassio-addons/stargazers)

![下载量趋势](https://raw.githubusercontent.com/alexbelgium/hassio-addons/master/emby/stats.png)

---

## 关于

[Emby](https://emby.media/) 可以整理视频、音乐、电视直播和照片等个人媒体库，并将其流式传输到智能电视、机顶盒和移动设备。此容器作为独立的 Emby 媒体服务器打包。

此插件基于 [linuxserver.io 提供的 docker 镜像](https://github.com/linuxserver/docker-emby)。
最初的插件版本来自：[https://github.com/petersendev/hassio-addons](https://github.com/petersendev/hassio-addons)

---

## 配置

Web 界面可通过 `<你的IP>:8096` 访问，或者在 Home Assistant 内通过 **Ingress** 打开。

### 配置选项

| 选项             | 类型   | 默认值     | 描述                                |
| -------------- | ---- | ------- | --------------------------------- |
| `PGID`         | int  | `0`     | 文件权限的组 ID                         |
| `PUID`         | int  | `0`     | 文件权限的用户 ID                        |
| `TZ`           | str  |         | 时区（例如 `Europe/London`）            |
| `localdisks`   | str  |         | 要挂载的本地磁盘（如 `sda1,sdb1,MYNAS`）     |
| `networkdisks` | str  |         | 要挂载的 SMB 网络共享（如 `//SERVER/SHARE`） |
| `cifsusername` | str  |         | SMB 用户名                           |
| `cifspassword` | str  |         | SMB 密码                            |
| `cifsdomain`   | str  |         | SMB 域                             |
| `smbv1`        | bool | `false` | 是否启用 SMB v1 协议                    |
| `silent`       | bool | `false` | 是否隐藏调试信息                          |

---

### 配置示例

```yaml
PGID: 0
PUID: 0
TZ: "Europe/London"
localdisks: "sda1,sdb1"
networkdisks: "//192.168.1.100/media,//nas.local/movies"
cifsusername: "mediauser"
cifspassword: "password123"
cifsdomain: "workgroup"
silent: false
```

---

### 磁盘挂载

此插件支持挂载 **本地磁盘** 和 **远程 SMB 共享**：

* **本地磁盘**：见 [插件中挂载本地磁盘](https://github.com/alexbelgium/hassio-addons/wiki/Mounting-Local-Drives-in-Addons)
* **远程共享**：见 [插件中挂载远程共享](https://github.com/alexbelgium/hassio-addons/wiki/Mounting-remote-shares-in-Addons)

---

## 安装

此插件的安装步骤与安装其他 Hass.io 插件类似：

1. [添加我的 Hass.io 插件仓库][repository] 到你的 Hass.io 实例。
2. 安装该插件。
3. 点击 **保存** 按钮存储你的配置。
4. 启动插件。
5. 查看插件日志确认是否运行正常。
6. 按需进一步配置插件，详见 Emby 官方文档。

[repository]: https://github.com/alexbelgium/hassio-addons

---

要不要我也帮你把 **Emby 插件文档**优化成更符合国内用户习惯的说明书（带详细步骤图解和 NAS/群晖场景示例）？
