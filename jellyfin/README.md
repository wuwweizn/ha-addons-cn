# Home Assistant 插件：Jellyfin

[![Donate][donation-badge]](https://www.buymeacoffee.com/alexbelgium)
[![Donate][paypal-badge]](https://www.paypal.com/donate/?hosted_button_id=DZFULJZTP3UQA)

![Version](https://img.shields.io/badge/dynamic/json?label=Version\&query=%24.version\&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Fjellyfin%2Fconfig.json)
![Ingress](https://img.shields.io/badge/dynamic/json?label=Ingress\&query=%24.ingress\&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Fjellyfin%2Fconfig.json)
![Arch](https://img.shields.io/badge/dynamic/json?color=success\&label=Arch\&query=%24.arch\&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Fjellyfin%2Fconfig.json)

[![Codacy Badge](https://app.codacy.com/project/badge/Grade/9c6cf10bdbba45ecb202d7f579b5be0e)](https://www.codacy.com/gh/alexbelgium/hassio-addons/dashboard?utm_source=github.com&utm_medium=referral&utm_content=alexbelgium/hassio-addons&utm_campaign=Badge_Grade)
[![GitHub Super-Linter](https://img.shields.io/github/actions/workflow/status/alexbelgium/hassio-addons/weekly-supelinter.yaml?label=Lint%20code%20base)](https://github.com/alexbelgium/hassio-addons/actions/workflows/weekly-supelinter.yaml)
[![Builder](https://img.shields.io/github/actions/workflow/status/alexbelgium/hassio-addons/onpush_builder.yaml?label=Builder)](https://github.com/alexbelgium/hassio-addons/actions/workflows/onpush_builder.yaml)

[donation-badge]: https://img.shields.io/badge/Buy%20me%20a%20coffee%20\(no%20paypal\)-%23d32f2f?logo=buy-me-a-coffee&style=flat&logoColor=white
[paypal-badge]: https://img.shields.io/badge/Buy%20me%20a%20coffee%20with%20Paypal-0070BA?logo=paypal&style=flat&logoColor=white

*感谢所有给我的仓库点赞的人！点击图片即可点赞，它会显示在右上角。*

[![Stargazers repo roster for @alexbelgium/hassio-addons](https://raw.githubusercontent.com/alexbelgium/hassio-addons/master/.github/stars2.svg)](https://github.com/alexbelgium/hassio-addons/stargazers)

![下载趋势](https://raw.githubusercontent.com/alexbelgium/hassio-addons/master/jellyfin/stats.png)

---

## 关于

[Jellyfin](https://jellyfin.org/) 可以管理个人媒体库中的视频、音乐、直播电视和照片，并将其流式传输到智能电视、流媒体盒子和移动设备。本插件打包了独立的 Jellyfin 媒体服务器容器。

此插件基于 [linuxserver.io 的 Docker 镜像](https://github.com/linuxserver/docker-jellyfin)。

---

## 配置

Web 界面可通过 `<你的-IP>:8096` 访问，也可以通过侧边栏的 Ingress 进入。

### 配置选项

| 选项              | 类型   | 默认                | 描述                              |
| --------------- | ---- | ----------------- | ------------------------------- |
| `PGID`          | int  | `0`               | 文件权限的组 ID                       |
| `PUID`          | int  | `0`               | 文件权限的用户 ID                      |
| `TZ`            | str  |                   | 时区（例如 `Europe/London`）          |
| `data_location` | str  | `/share/jellyfin` | Jellyfin 数据存储路径                 |
| `localdisks`    | str  |                   | 本地挂载的磁盘（例如 `sda1,sdb1,MYNAS`）   |
| `networkdisks`  | str  |                   | SMB 网络共享挂载（例如 `//SERVER/SHARE`） |
| `cifsusername`  | str  |                   | 网络共享用户名                         |
| `cifspassword`  | str  |                   | 网络共享密码                          |
| `cifsdomain`    | str  |                   | 网络共享域名                          |
| `DOCKER_MODS`   | list |                   | 硬件加速的额外 Docker 模块               |

### 配置示例

```yaml
PGID: 0
PUID: 0
TZ: "Europe/London"
data_location: "/share/jellyfin"
localdisks: "sda1,sdb1"
networkdisks: "//192.168.1.100/media,//nas.local/movies"
cifsusername: "mediauser"
cifspassword: "password123"
cifsdomain: "workgroup"
DOCKER_MODS:
  - "linuxserver/mods:jellyfin-opencl-intel"
  - "linuxserver/mods:jellyfin-amd"
```

### 硬件加速

可用 Docker 模块：

* `linuxserver/mods:jellyfin-opencl-intel` - Intel OpenCL 支持
* `linuxserver/mods:jellyfin-amd` - AMD 硬件加速
* `linuxserver/mods:jellyfin-rffmpeg` - 自定义 FFmpeg 构建

### 挂载磁盘

支持挂载本地磁盘和远程 SMB 共享：

* **本地磁盘**：[本地磁盘挂载指南](https://github.com/alexbelgium/hassio-addons/wiki/Mounting-Local-Drives-in-Addons)
* **远程共享**：[远程共享挂载指南](https://github.com/alexbelgium/hassio-addons/wiki/Mounting-remote-shares-in-Addons)

### 自定义脚本与环境变量

可通过 `addon_config` 映射使用自定义脚本和环境变量：

* **自定义脚本**：[在插件中运行自定义脚本](https://github.com/alexbelgium/hassio-addons/wiki/Running-custom-scripts-in-Addons)
* **环境变量**：[向插件添加环境变量](https://github.com/alexbelgium/hassio-addons/wiki/Add-Environment-variables-to-your-Addon)

---

### 启用 SSL

#### 创建 PFX 证书文件

1. 假设你已经通过 Let's Encrypt 插件生成了 PEM 格式证书
2. 运行命令：

```bash
openssl pkcs12 -export -in fullchain.pem -inkey private_key.pem -passout pass: -out server.pfx
```

3. 设置权限：

```bash
chmod 0700 server.pfx
```

> 注意：上面的命令生成了无密码的 PFX 文件，你也可以通过 `-passout pass:"your-password"` 设置密码，但在 Jellyfin 配置中需填写该密码

#### 自动化生成 PFX

（可根据需求自行脚本化处理）

#### Jellyfin 配置

1. 在侧边栏点击 `Administration` -> `Dashboard`
2. 在 `Networking` 下的 `Server Address Settings` 勾选 `Enable HTTPS`
3. 在 `HTTPS Settings` 勾选 `Require HTTPS`
4. 对于 `Custom SSL certificate path:` 指向 PFX 文件，并在需要时填写证书密码
5. 滚动到页面底部并点击 `Save`

---

## 安装

安装过程与其他 Hass.io 插件类似：

1. 将 [Hass.io 插件仓库][repository] 添加到 Hass.io
2. 安装此插件
3. 点击 `Save` 保存配置
4. 启动插件
5. 查看插件日志，确认启动正常
6. 按照官方文档仔细配置插件

[repository]: https://github.com/alexbelgium/hassio-addons
