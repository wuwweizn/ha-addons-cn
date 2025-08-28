# Home Assistant 社区插件：WireGuard

[WireGuard®][wireguard] 是一个极其简单但快速、现代化的 VPN，采用最先进的加密技术。它旨在比 IPsec 更快、更简单、更轻量且更实用，同时避免复杂的配置问题。

WireGuard 的性能通常优于 OpenVPN。它被设计为通用 VPN，可在嵌入式设备和超级计算机上运行，适用于多种使用场景。

最初发布于 Linux 内核，现在已跨平台（Windows、macOS、BSD、iOS、Android）并可广泛部署，包括通过 Hass.io 插件安装。

WireGuard 仍在积极开发中，但已经可以被认为是业内最安全、最易用、最简单的 VPN 解决方案之一。

## 安装

WireGuard 本身相对简单，但对于不熟悉相关术语的用户可能会有些复杂。该插件会帮你处理很多配置（如果你希望的话）。

安装及快速开始步骤如下：

1. 点击下面的 Home Assistant 我的按钮，在你的 Home Assistant 实例中打开插件。

   [![在 Home Assistant 实例中打开此插件][addon-badge]][addon]

2. 点击“Install”安装插件。

3. 在配置中设置 `host` 为你的 Home Assistant 外部地址，例如 `myautomatedhome.duckdns.org`。

4. 将 peer（客户端）名称改为有意义的名称，例如 `myphone`。

5. 保存配置。

6. 启动 “WireGuard” 插件。

7. 检查插件日志，确认一切正常。

8. 在路由器中将端口 `51820`（UDP）转发到 Home Assistant。

9. 下载或打开 `/ssl/wireguard/myphone/qrcode.png` 文件（可通过 Samba、VS Code 或 Configurator 插件）。

10. 在手机上安装 WireGuard 应用。

11. 扫描二维码添加新的 WireGuard 连接。

12. 连接成功！

## 配置

WireGuard 配置选项较多，但插件只要求设置少数几个简单选项，其余由插件处理。若想进行复杂配置，也可在插件中设置。

### 服务器配置示例

```yaml
log_level: info
server:
  host: myautomatedhome.duckdns.org
  addresses:
    - 10.10.10.1
  dns:
    - 1.1.1.1
    - 1.0.0.1
peers:
  - name: frenck
    addresses:
      - 10.10.10.2
    allowed_ips: []
    client_allowed_ips: []
```

**注意**：示例仅供参考，请根据实际情况创建自己的配置。

### 重要选项说明

* `server.host`：客户端连接使用的主机名或 IP，不包含端口。
* `server.addresses`：分配给服务器的 IP 列表，建议与家庭网络 IP 不重叠。
* `server.dns`（可选）：用于服务器和客户端的 DNS。
* `server.private_key` / `server.public_key`（可选）：可手动提供密钥，否则插件会生成。
* `peers.name`：客户端名称，用于生成配置和 QR 码。
* `peers.addresses`：分配给客户端的 IP 列表。
* `peers.allowed_ips` / `peers.client_allowed_ips`：指定允许的流量源或目标 IP。
* `peers.endpoint`（可选）：客户端连接服务器的地址。
* `log_level`：日志级别，可选 `trace`、`debug`、`info`、`warning`、`error`、`fatal`。

更多可选高级配置包括 `server.pre_up`、`server.post_up`、`server.post_down`、`peers.persistent_keep_alive` 等。

## 生成的客户端配置

所有生成文件存储在 `/ssl/wireguard`，每个客户端独立文件夹，并生成包含二维码的图片，方便快速配置手机或其他设备。

## Linux/Debian/Ubuntu Hass.io 系统使用

HassOS 默认内核支持 WireGuard。如果在普通 Linux 上运行 Hass.io，插件会使用用户空间的 WireGuard 实现，性能略低。建议在宿主机安装 WireGuard：

### Ubuntu

```bash
sudo add-apt-repository ppa:wireguard/wireguard
sudo apt-get update
sudo apt-get install wireguard
```

### Debian

```bash
sudo echo "deb http://deb.debian.org/debian/ unstable main" > /etc/apt/sources.list.d/unstable.list
sudo printf 'Package: *\nPin: release a=unstable\nPin-Priority: 90\n' > /etc/apt/preferences.d/limit-unstable
sudo apt update
sudo apt install wireguard
```

### Fedora

```bash
sudo dnf copr enable jdoss/wireguard
sudo dnf install wireguard-dkms wireguard-tools
```

### 其他系统

请参考 [WireGuard 安装手册][wireguard-install]。

## 常见问题提示

* **“Missing WireGuard kernel module…”**：请参考上文 Linux 系统安装部分。
* **“IP forwarding is disabled on the host system!”**：启用 IP 转发：

```bash
sudo sysctl -w net.ipv4.ip_forward=1
echo "net.ipv4.ip_forward = 1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p /etc/sysctl.conf
```

## 备份

使用 Home Assistant 备份插件可备份 WireGuard 插件，但生成的客户端配置（包括密钥）需单独备份 `/ssl/wireguard` 文件夹。

## 支持 API

插件提供一个简单的 WireGuard 状态 API，可通过 Home Assistant 的 RESTful 集成获取信息：

```yaml
sensor:
  - platform: rest
    resource: http://a0d7b954-wireguard
```

## 支持与帮助

* [Home Assistant 社区插件 Discord][discord]
* [Home Assistant Discord][discord-ha]
* [Home Assistant 社区论坛][forum]
* [Reddit /r/homeassistant][reddit]
* [GitHub 问题反馈][issue]

## 作者及贡献者

原作者：[Franck Nijhof][frenck]
完整贡献者列表：[contributors][contributors]

## 许可协议

MIT License

版权所有 (c) 2019-2025 Franck Nijhof

允许免费使用、复制、修改、合并、发布、分发、再许可及销售软件及文档，须包含版权声明及许可声明。

软件按“原样”提供，不保证任何形式的明示或暗示担保。

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_wireguard&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[adguard]: https://github.com/hassio-addons/addon-adguard-home
[contributors]: https://github.com/hassio-addons/addon-wireguard/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord]: https://discord.me/hassioaddons
[forum]: https://community.home-assistant.io/t/home-assistant-community-add-on-wireguard/134662?u=frenck
[frenck]: https://github.com/frenck
[ha-rest]: https://www.home-assistant.io/integrations/rest/
[issue]: https://github.com/hassio-addons/addon-wireguard/issues
[reddit]: https://reddit.com/r/homeassistant
[releases]: https://github.com/hassio-addons/addon-wireguard/releases
[semver]: https://semver.org/spec/v2.0.0.html
[wireguard-install]: https://www.wireguard.com/install/
[wireguard]: https://www.wireguard.com
