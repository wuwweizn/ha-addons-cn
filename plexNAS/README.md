
## ⚠️ 未解决问题： [🐛 \[PLEX\] 挂载错误（开启于 2025-08-05）](https://github.com/alexbelgium/hassio-addons/issues/2006) 由 [@jgunther-provenir](https://github.com/jgunther-provenir) 提出

# Home Assistant 插件：Plex

[![捐赠][donation-badge]](https://www.buymeacoffee.com/alexbelgium)
[![捐赠][paypal-badge]](https://www.paypal.com/donate/?hosted_button_id=DZFULJZTP3UQA)

![版本](https://img.shields.io/badge/dynamic/json?label=Version\&query=%24.version\&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Fplex%2Fconfig.json)
![入口](https://img.shields.io/badge/dynamic/json?label=Ingress\&query=%24.ingress\&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Fplex%2Fconfig.json)
![架构](https://img.shields.io/badge/dynamic/json?color=success\&label=Arch\&query=%24.arch\&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Fplex%2Fconfig.json)

[![Codacy 评分](https://app.codacy.com/project/badge/Grade/9c6cf10bdbba45ecb202d7f579b5be0e)](https://www.codacy.com/gh/alexbelgium/hassio-addons/dashboard?utm_source=github.com&utm_medium=referral&utm_content=alexbelgium/hassio-addons&utm_campaign=Badge_Grade)
[![GitHub Super-Linter](https://img.shields.io/github/actions/workflow/status/alexbelgium/hassio-addons/weekly-supelinter.yaml?label=Lint%20code%20base)](https://github.com/alexbelgium/hassio-addons/actions/workflows/weekly-supelinter.yaml)
[![构建](https://img.shields.io/github/actions/workflow/status/alexbelgium/hassio-addons/onpush_builder.yaml?label=Builder)](https://github.com/alexbelgium/hassio-addons/actions/workflows/onpush_builder.yaml)

[donation-badge]: https://img.shields.io/badge/Buy%20me%20a%20coffee%20\(no%20paypal\)-%23d32f2f?logo=buy-me-a-coffee&style=flat&logoColor=white
[paypal-badge]: https://img.shields.io/badge/Buy%20me%20a%20coffee%20with%20Paypal-0070BA?logo=paypal&style=flat&logoColor=white

*感谢每一位给我的仓库加星的人！点击下方图片即可加星，星会显示在右上角，谢谢！*

[![@alexbelgium/hassio-addons 仓库的 Stargazers](https://raw.githubusercontent.com/alexbelgium/hassio-addons/master/.github/stars2.svg)](https://github.com/alexbelgium/hassio-addons/stargazers)

![下载量变化](https://raw.githubusercontent.com/alexbelgium/hassio-addons/master/plex/stats.png)

---

## 关于

该插件是 fork 版本，增加了最新 Beta 版本、SMB 和本地硬盘挂载功能。

* 初始版本： [https://github.com/petersendev/hassio-addons](https://github.com/petersendev/hassio-addons)
* CIFS 代码： [https://github.com/dianlight/hassio-addons](https://github.com/dianlight/hassio-addons)

[Plex](https://plex.media/) 可组织个人媒体库中的视频、音乐、直播电视和照片，并将其流式传输到智能电视、流媒体盒子和移动设备。
该容器打包为独立的 Plex 媒体服务器。

本插件基于 linuxserver.io 的 [docker 镜像](https://github.com/linuxserver/docker-plex)。

---

## 配置

Web 界面访问地址：`<your-ip>:32400`

### 配置选项

| 选项                       | 类型   | 默认值     | 描述                                                                |
| ------------------------ | ---- | ------- | ----------------------------------------------------------------- |
| `PGID`                   | int  | `0`     | 文件权限组 ID                                                          |
| `PUID`                   | int  | `0`     | 文件权限用户 ID                                                         |
| `TZ`                     | str  |         | 时区（如 `Europe/London`）                                             |
| `claim`                  | str  |         | Plex claim 令牌（来自 [https://plex.tv/claim）](https://plex.tv/claim）) |
| `localdisks`             | str  |         | 要挂载的本地硬盘（如 `sda1,sdb1,MYNAS`）                                     |
| `networkdisks`           | str  |         | 要挂载的 SMB 网络共享（如 `//SERVER/SHARE`）                                 |
| `cifsusername`           | str  |         | 网络共享的 SMB 用户名                                                     |
| `cifspassword`           | str  |         | 网络共享的 SMB 密码                                                      |
| `cifsdomain`             | str  |         | 网络共享的 SMB 域                                                       |
| `smbv1`                  | bool | `false` | 是否启用 SMB v1 协议                                                    |
| `skip_permissions_check` | bool | `false` | 是否跳过文件权限检查                                                        |

### 配置示例

```yaml
PGID: 0
PUID: 0
TZ: "Europe/London"
claim: "从 https://www.plex.tv/claim 获取"
localdisks: "sda1,sdb1"
networkdisks: "//192.168.1.100/media,//nas.local/movies"
cifsusername: "mediauser"
cifspassword: "password123"
cifsdomain: "workgroup"
```

---

### 硬盘挂载

此插件支持挂载本地硬盘和远程 SMB 共享：

* **本地硬盘**：见 [插件中挂载本地硬盘](https://github.com/alexbelgium/hassio-addons/wiki/Mounting-Local-Drives-in-Addons)
* **远程共享**：见 [插件中挂载远程共享](https://github.com/alexbelgium/hassio-addons/wiki/Mounting-remote-shares-in-Addons)

---

## 安装

安装此插件非常简单，与安装其他 Hass.io 插件类似：

1. 将 [我的 Hass.io 插件仓库][repository] 添加到你的 Hass.io 实例。
2. 安装此插件。
3. 点击 `保存` 按钮保存配置。
4. 启动插件。
5. 查看插件日志，确认是否一切正常。
6. 根据官方文档仔细配置插件以符合个人需求。

[repository]: https://github.com/alexbelgium/hassio-addons


