# Home Assistant 社区插件：Tailscale

Tailscale 是一款“零配置”VPN，可在几分钟内安装到任何设备上，包括你的 Home Assistant 实例。

它可以在服务器、计算机和云实例之间创建一个安全的网络。即使设备处于不同防火墙或子网下，Tailscale 也能正常工作。Tailscale 会自动管理防火墙规则，并可随时随地使用。

## 前提条件

要使用此插件，你需要拥有一个 Tailscale 账号。

个人及爱好项目可免费使用，单个用户账户最多支持 100 个客户端/设备。可使用 Google、Microsoft 或 GitHub 账号注册：

[https://login.tailscale.com/start](https://login.tailscale.com/start)

你也可以在安装插件过程中创建账户，但提前了解注册流程会更方便。

## 安装步骤

1. 点击下方按钮，在你的 Home Assistant 中打开该插件：

   [![在 Home Assistant 中打开此插件][addon-badge]][addon]

2. 点击“安装”按钮安装插件。

3. 启动“Tailscale”插件。

4. 查看“Tailscale”插件日志，确认安装正常。

5. 打开插件 Web 界面，完成身份验证，将 Home Assistant 与 Tailscale 账户绑定。
   \*\*注意：\*\*某些浏览器可能无法完成此步骤，建议在桌面或笔记本电脑上使用 Chrome 浏览器。

6. 再次查看插件日志，确认一切正常。

7. 完成！

## 配置

此插件本身几乎不需要额外配置。

不过，在登录 Tailscale 后，你可以在其界面中配置你的 Tailscale 网络。

[https://login.tailscale.com/](https://login.tailscale.com/)

插件支持“出口节点”功能，可在 Tailscale 账户中启用。此外，如果你的网络由 Supervisor 管理（默认情况），插件会在所有支持的接口上向 Tailscale 广告你的子网路由。

建议禁用密钥过期，以避免丢失 Home Assistant 设备的连接。详情请参考 [Key expiry][tailscale_info_key_expiry]。

```yaml
accept_dns: true
accept_routes: true
advertise_exit_node: true
advertise_connector: true
advertise_routes:
  - 192.168.1.0/24
  - fd12:3456:abcd::/64
funnel: false
log_level: info
login_server: "https://controlplane.tailscale.com"
proxy: false
proxy_and_funnel_port: 443
snat_subnet_routes: true
stateful_filtering: false
tags:
  - tag:example
  - tag:homeassistant
taildrop: true
userspace_networking: true
```

> **注意：**
> 插件中某些配置选项也可通过 Tailscale Web UI 查看，但为只读状态。Web UI 无法修改这些选项，因为插件重启后所有更改会丢失。

---

### 选项说明

#### `accept_dns`

如果你在此设备上使用 MagicDNS 遇到问题，可以通过此选项禁用。默认启用。

如果你的设备运行 Pi-hole 或 AdGuard Home，MagicDNS 可能会产生冲突。此时可禁用 `accept_dns`，仍可在网络其他设备上使用 MagicDNS，将 `100.100.100.100` 设置为 DNS 即可。

#### `accept_routes`

是否接受其他 Tailscale 节点广告的子网路由。默认启用。
更多信息：[Subnet routers][tailscale_info_subnets]。

#### `advertise_exit_node`

是否将此设备作为出口节点供其他节点使用，用于路由互联网流量（类似 VPN）。默认启用。
更多信息：[Exit nodes][tailscale_info_exit_nodes]。

#### `advertise_connector`

是否将此设备作为应用连接器 (app connector) 广告。可指定应用域名，将流量通过 Tailscale 路由到指定节点。默认启用。
更多信息：[App connectors][tailscale_info_app_connectors]。

#### `advertise_routes`

是否向其他 Tailscale 客户端广播本地网络的子网路由。默认情况下，插件会在所有支持接口上广播子网路由。
如不需要，可设置为空列表 `[]`。
更多信息：[Subnet routers][tailscale_info_subnets]。

#### `funnel`

需要开启 Tailscale Proxy。
启用后，可通过 Tailscale 域名（如 `https://homeassistant.tail1234.ts.net`）从互联网访问 Home Assistant，即使设备未安装 Tailscale VPN。
默认禁用。
更多信息：[Tailscale Funnel][tailscale_info_funnel]。

#### `log_level`

控制插件日志级别，便于调试。默认 `info`。可选值：

* `trace`：显示所有细节
* `debug`：详细调试信息
* `info`：一般事件
* `notice`：普通重要事件
* `warning`：异常事件
* `error`：运行时错误
* `fatal`：严重错误，插件不可用

#### `login_server`

指定自定义控制服务器，例如自建 [Headscale] 实例。默认使用 `https://controlplane.tailscale.com`。

#### `proxy`

启用 Tailscale TLS 证书，为 Home Assistant 提供 HTTPS 支持。默认禁用。
需在 `configuration.yaml` 中添加：

```yaml
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 127.0.0.1
```

更多信息：[启用 HTTPS][tailscale_info_https]。

#### `proxy_and_funnel_port`

配置 Tailscale Proxy 与 Funnel 功能使用的端口（仅允许 443、8443 和 10000）。默认 443。

#### `snat_subnet_routes`

是否对子网设备显示真实流量来源 IP，简化路由配置。默认启用。

#### `stateful_filtering`

启用状态包过滤，仅允许已建立连接的返回包。默认禁用。

#### `tags`

为此设备添加 Tailscale 标签，格式需以 `tag:` 开头。
更多信息：[Tags][tailscale_info_tags]。

#### `taildrop`

启用 Tailscale Taildrop 功能，从其他 Tailscale 设备发送文件到 Home Assistant。
接收的文件存储在 `/share/taildrop`。默认启用。
更多信息：[Taildrop][taildrop]。

#### `userspace_networking`

启用用户空间网络模式，使 Home Assistant 及本地子网在 Tailnet 内可访问。默认启用。
禁用后会创建 `tailscale0` 网络接口，可访问 Tailnet 内的其他客户端。

---

## 网络端口

### `41641/udp`

WireGuard 及 P2P 流量端口。
如在 CGNAT 网络无法建立 P2P 连接，可通过路由器端口转发解决。

---

## 更新日志与版本

版本遵循 [语义化版本][semver]：

* `MAJOR`：不兼容或重大更改
* `MINOR`：向后兼容的新功能或增强
* `PATCH`：向后兼容的修复或更新

更多信息请查看 [GitHub Releases][releases]。

---

## 支持

如有疑问，可通过以下渠道获取帮助：

* [Home Assistant 社区插件 Discord][discord]
* [Home Assistant 官方 Discord][discord-ha]
* [Home Assistant 社区论坛][forum]
* [Reddit /r/homeassistant][reddit]
* 在 GitHub [开 issue][issue]

---

## 作者与贡献者

原始仓库由 [Franck Nijhof][frenck] 创建。
完整贡献者列表请查看 [贡献者页面][contributors]。

---

## 许可证

MIT 许可证

版权所有 (c) 2021-2025 Franck Nijhof

允许在遵守 MIT 许可证的前提下自由使用、修改、发布和分发本软件。

---

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_tailscale&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[contributors]: https://github.com/hassio-addons/addon-tailscale/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord]: https://discord.me/hassioaddons
[forum]: https://community.home-assistant.io/?u=frenck
[frenck]: https://github.com/frenck
[headscale]: https://github.com/juanfont/headscale
[http_integration]: https://www.home-assistant.io/integrations/http/
[issue]: https://github.com/hassio-addons/addon-tailscale/issues
[reddit]: https://reddit.com/r/homeassistant
[releases]: https://github.com/hassio-addons/addon-tailscale/releases
[semver]: https://semver.org/spec/v2.0.0.html
[taildrop]: https://tailscale.com/taildrop
[tailscale_acls]: https://login.tailscale.com/admin/acls
[tailscale_dns]: https://login.tailscale.com/admin/dns
[tailscale_info_exit_nodes]: https://tailscale.com/kb/1103/exit-nodes
[tailscale_info_app_connectors]: https://tailscale.com/kb/1281/app-connectors
[tailscale_info_funnel]: https://tailscale.com/kb/1223/funnel
[tailscale_info_funnel_policy_requirement]: https://tailscale.com/kb/1223/funnel#requirements-and-limitations
[tailscale_info_https]: https://tailscale.com/kb/1153/enabling-https
[tailscale_info_key_expiry]: https://tailscale.com/kb/1028/key-expiry
[tailscale_info_site_to_site]: https://tailscale.com/kb/1214/site-to-site
[tailscale_info_subnets]: https://tailscale.com/kb/1019/subnets
[tailscale_info_tags]: https://tailscale.com/kb/1068/tags
[tailscale_info_userspace_networking]: https://tailscale.com/kb/1112/userspace-networking

