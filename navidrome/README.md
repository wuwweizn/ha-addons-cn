# Home Assistant 插件：Navidrome

[!\[捐赠\]\[donation-badge\]](https://www.buymeacoffee.com/alexbelgium)
[!\[捐赠\]\[paypal-badge\]](https://www.paypal.com/donate/?hosted_button_id=DZFULJZTP3UQA)

![版本](https://img.shields.io/badge/dynamic/json?label=Version\&query=%24.version\&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Fnavidrome%2Fconfig.json)
![支持 Ingress](https://img.shields.io/badge/dynamic/json?label=Ingress\&query=%24.ingress\&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Fnavidrome%2Fconfig.json)
![架构](https://img.shields.io/badge/dynamic/json?color=success\&label=Arch\&query=%24.arch\&url=https%3A%2F%2Fraw.githubusercontent.com%2Falexbelgium%2Fhassio-addons%2Fmaster%2Fnavidrome%2Fconfig.json)

*感谢所有给我的仓库点星的朋友！点击下面的图标即可点星，星标会显示在右上角。谢谢！*

[![Stargazers for @alexbelgium/hassio-addons](https://raw.githubusercontent.com/alexbelgium/hassio-addons/master/.github/stars2.svg)](https://github.com/alexbelgium/hassio-addons/stargazers)

![下载趋势](https://raw.githubusercontent.com/alexbelgium/hassio-addons/master/navidrome/stats.png)

## 关于

Navidrome 是一款音乐服务器，这个插件提供了额外的配置选项和优化。
该插件基于 [Docker 镜像](https://hub.docker.com/r/deluan/navidrome)。

Web 界面可通过 `<http://homeassistant:PORT>` 访问，或通过侧边栏使用 Ingress。
大部分配置可以直接通过应用的 Web 界面完成，以下选项需在插件配置中设置。
更多配置详情请参考官方文档： [Navidrome 配置选项](https://www.navidrome.org/docs/usage/configuration-options/)

## 配置选项

| 选项                        | 类型   | 默认值           | 描述                                |
| ------------------------- | ---- | ------------- | --------------------------------- |
| `base_url`                | str  | `/`           | 配置 Navidrome 代理的基础 URL            |
| `music_folder`            | str  | `/data/music` | 音乐库所在文件夹                          |
| `data_folder`             | str  | `/data`       | 存放应用数据（数据库）的文件夹                   |
| `log_level`               | str  | `info`        | 日志等级（error、warn、info、debug、trace） |
| `ssl`                     | bool | `false`       | 是否启用 HTTPS                        |
| `certfile`                | str  |               | TLS 证书路径                          |
| `keyfile`                 | str  |               | TLS 密钥路径                          |
| `default_language`        | str  |               | 界面默认语言                            |
| `image_cache_size`        | str  |               | 图片缓存大小                            |
| `transcoding_cache_size`  | str  |               | 转码缓存大小                            |
| `scan_schedule`           | str  |               | 自动扫描库的 Cron 表达式                   |
| `password_encryption_key` | str  |               | 密码加密密钥                            |
| `welcome_message`         | str  |               | 自定义欢迎信息                           |
| `lastfm_api_key`          | str  |               | Last.fm API 密钥，用于 scrobbling      |
| `lastfm_secret`           | str  |               | Last.fm secret，用于 scrobbling      |
| `spotify_id`              | str  |               | Spotify 客户端 ID，用于元数据              |
| `spotify_secret`          | str  |               | Spotify 客户端 Secret，用于元数据          |
| `localdisks`              | str  |               | 本地挂载的磁盘（如 `sda1,sdb1,MYNAS`）      |
| `networkdisks`            | str  |               | SMB 网络共享（如 `//SERVER/SHARE`）      |
| `cifsusername`            | str  |               | SMB 用户名                           |
| `cifspassword`            | str  |               | SMB 密码                            |
| `cifsdomain`              | str  |               | SMB 域名                            |

### 示例配置

```yaml
base_url: "/"
music_folder: "/data/music"
data_folder: "/data"
log_level: "info"
ssl: false
certfile: "fullchain.pem"
keyfile: "privkey.pem"
scan_schedule: "0 2 * * *"
lastfm_api_key: "your-lastfm-key"
localdisks: "sda1,sdb1"
networkdisks: "//192.168.1.100/music"
cifsusername: "musicuser"
cifspassword: "password123"
cifsdomain: "workgroup"
```

### 挂载磁盘

此插件支持挂载本地磁盘和远程 SMB 网络共享：

* **本地磁盘**：参见 [Add-ons 中挂载本地磁盘](https://github.com/alexbelgium/hassio-addons/wiki/Mounting-Local-Drives-in-Addons)
* **远程共享**：参见 [Add-ons 中挂载远程共享](https://github.com/alexbelgium/hassio-addons/wiki/Mounting-remote-shares-in-Addons)

### 自定义脚本和环境变量

此插件支持自定义脚本和环境变量：

* **自定义脚本**：参见 [在 Add-ons 中运行自定义脚本](https://github.com/alexbelgium/hassio-addons/wiki/Running-custom-scripts-in-Addons)
* **环境变量**：参见 [为插件添加环境变量](https://github.com/alexbelgium/hassio-addons/wiki/Add-Environment-variables-to-your-Addon)

## 安装步骤

安装此插件与其他 Hass.io 插件类似：

1. 将我的 Hass.io 插件仓库 [添加到 Hass.io](https://github.com/alexbelgium/hassio-addons)。
2. 安装 Navidrome 插件。
3. 点击 `保存` 按钮保存配置。
4. 启动插件。
5. 查看插件日志确认运行状态。
6. 打开 Web 界面初始化应用。
7. 重启插件以应用任何需要生效的选项。
