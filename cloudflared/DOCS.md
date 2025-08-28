
# Home Assistant 插件：Cloudflared

Cloudflared 通过安全隧道将你的 Home Assistant 实例连接到 Cloudflare 的域名或子域名。
这允许你在不打开路由器端口的情况下，将 Home Assistant 实例和其他服务暴露到互联网。此外，你还可以利用 Cloudflare Zero Trust 来进一步保护你的连接。

## 免责声明

使用此插件时，请确保遵守 \[Cloudflare 自助订阅协议]\[cloudflare-sssa]。

## 初始设置

### 前提条件

1. 一个使用 Cloudflare DNS 的域名（例如 example.com）。如果没有，请参阅 \[域名和 Cloudflare 设置]\[how-tos]。
   请注意，**Freenom** 的域名不再适用，因此你需要选择或迁移到其他注册商。
2. 如果尚未启用，请在 Cloudflare 为你的域名 \[激活 Websockets]\[cloudflare-websockets]。
3. 决定使用本地隧道（由插件管理）还是远程隧道（通过 Cloudflare 界面管理）。\[了解更多]\[addon-remote-or-local]。
4. 此插件应已[安装][addon-installation]但尚未启动。

完成前提条件后，根据你选择的隧道类型继续以下步骤。

### 本地隧道插件设置（推荐）

在以下步骤中，插件将自动创建一个 Cloudflare 隧道来暴露你的 Home Assistant 实例。

如果你只想暴露其他服务，可以将 `external_hostname` 留空，并按照下文[描述](#configuration)设置 `additional_hosts`。

1. 在 Home Assistant 配置中设置 `http` 集成，如下文[描述](#configurationyaml)。
2. 将插件选项 `external_hostname` 设置为你想用于远程访问的域名/子域名，例如 `ha.example.com`。
3. 启动插件（这将覆盖所有与 `external_hostname` 或 `additional_hosts` 匹配的现有 DNS 条目）。
4. 在新标签页中粘贴插件日志中的 URL，以完成 Cloudflare 身份验证。
5. 通过远程 URL 访问 Home Assistant，例如 `https://ha.example.com/`，无需端口号。

现在，你的隧道应已在 Cloudflare Teams 控制面板中列出。请查看下方的其他配置选项。

### 远程隧道插件设置（高级）

在以下步骤中，你需要手动在 Cloudflare Zero Trust 控制面板创建隧道，并将 token 提供给插件。

1. 在 Home Assistant 配置中设置 `http` 集成，如下文[描述](#configurationyaml)。
2. 按照 [此教程][addon-remote-tunnel] 在 Cloudflare Teams 控制面板创建隧道。
3. 将插件选项 `tunnel_token` 设置为你的\[隧道 token]\[create-remote-managed-tunnel]（其他配置将被忽略）。
4. 启动插件，并检查日志以确认一切正常。
5. 通过远程 URL 访问 Home Assistant，例如 `https://ha.example.com/`，无需端口号。

你的隧道现在应已与 Cloudflared 插件关联。任何配置更改应在 Cloudflare Teams 控制面板中进行。

## 配置

**这些配置选项仅适用于本地隧道设置**。使用远程隧道可实现更高级的配置。

* [`external_hostname`](#option-external_hostname)
* [`additional_hosts`](#option-additional_hosts)
* [`tunnel_name`](#option-tunnel_name)
* [`catch_all_service`](#option-catch_all_service)
* [`nginx_proxy_manager`](#option-nginx_proxy_manager)
* [`use_builtin_proxy`](#option-use_builtin_proxy)
* [`post_quantum`](#option-post_quantum)
* [`run_parameters`](#option-run_parameters)
* [`log_level`](#option-log_level)

### 插件配置概览

**注意**：*更改配置后，请记得重启插件。*

示例插件配置：

```yaml
external_hostname: ha.example.com
additional_hosts:
  - hostname: router.example.com
    service: http://192.168.1.1
  - hostname: website.example.com
    service: http://192.168.1.3:8080
```

**注意**：*这只是示例，请不要直接复制粘贴！请创建自己的配置！*

### 选项：`external_hostname`

设置 `external_hostname` 为你希望访问 Home Assistant 的域名或子域名。

此项可选，如果只想暴露其他服务，可以使用 `additional_hosts`。

**注意**：*隧道名称在你的 Cloudflare 账户中必须唯一。*

```yaml
external_hostname: ha.example.com
```

### 选项：`additional_hosts`

你可以使用 Cloudflare 隧道的内部反向代理来定义除了 Home Assistant 外的其他主机，从而通过隧道访问磁盘站、路由器等系统。

与 `external_hostname` 类似，DNS 条目会自动在 Cloudflare 创建。

你可以为某个主机添加可选项 `disableChunkedEncoding` 来禁用分块传输编码，这在运行 WSGI 服务器（例如 Proxmox）时非常有用。更多信息请参阅 \[Cloudflare 文档]\[disablechunkedencoding]。

示例配置：

```yaml
additional_hosts:
  - hostname: router.example.com
    service: http://192.168.1.1
  - hostname: diskstation.example.com
    service: https://192.168.1.2:5001
  - hostname: website.example.com
    service: http://192.168.1.3:8080
    disableChunkedEncoding: true
```

**注意 1**：*如果从列表中删除主机名，它将不再提供服务，但你仍需手动从 Cloudflare 删除相应 DNS 条目。*

**注意 2**：*如果想完全删除 `additional_hosts`，请在配置中添加空数组：*

```yaml
additional_hosts: []
```

### 选项：`tunnel_name`

设置隧道名称，默认是 `homeassistant`。

**注意**：*隧道名称在 Cloudflare 账户中必须唯一。*

```yaml
tunnel_name: myHomeAssistant
```

### 选项：`catch_all_service`

将所有未在 `external_hostname` 或 `additional_hosts` 中定义的请求转发到指定 URL，例如可用于反向代理。

**注意**：*如果使用 HA 插件 \[Nginx Proxy Manager]\[nginx\_proxy\_manager] 作为反向代理，应设置 `nginx_proxy_manager`（见下文），不要使用此选项。*

```yaml
catch_all_service: http://192.168.1.100
```

**说明**：*定义的 `external_hostname` 会路由到 Home Assistant，`additional_hosts` 也会路由到配置的服务，其他流量会转发到 `catch_all_service`。*

路由主机名时，需要在 Cloudflare 为每个主机创建 CNAME 记录，指向 `external_hostname` 或直接指向隧道 URL。

也可通过添加通配符 DNS 记录（CNAME 名称为 `*`）实现。

### 选项：`nginx_proxy_manager`

启用后，可让 Cloudflare 隧道与 \[Nginx Proxy Manager]\[nginx\_proxy\_manager] 配合使用。
插件会自动将 `catch_all_service` 设置为 Nginx Proxy Manager 的内部 URL，无需手动添加 `catch_all_service`。

```yaml
nginx_proxy_manager: true
```

**说明**：*与 `catch_all_service` 相同，定义的 `external_hostname` 和 `additional_hosts` 仍会路由到配置服务，其他流量会路由到 Nginx Proxy Manager。*

路由主机名时，需要在 Cloudflare 为每个主机创建 CNAME 记录，指向 `external_hostname` 或直接指向隧道 URL。

然后在 Nginx Proxy Manager 中设置代理主机，将流量转发到目标服务。

### 选项：`use_builtin_proxy`

启用后，连接 Home Assistant 将通过内置 Nginx 代理进行。
Nginx 作为解决实时日志问题的替代方案实现。
参考讨论 [#744](https://github.com/brenner-tobias/addon-cloudflared/discussions/744)。

**说明**：*此选项默认启用。*

### 选项：`post_quantum`

启用后，Cloudflared 会使用后量子加密进行隧道通信。

**说明**：*启用 `post_quantum` 时，隧道连接仅使用 QUIC 协议，可能导致部分用户出现问题。同时，只允许后量子混合密钥交换，不会回退到非后量子连接。*

```yaml
post_quantum: true
```

### 选项：`run_parameters`

可以为 cloudflared 守护进程添加额外运行参数。
参考 \[Cloudflare 文档]\[cloudflare-run\_parameter] 获取可用参数及说明。

有效参数示例：

* \--edge-bind-address
* \--edge-ip-version
* \--grace-period
* \--logfile
* \--loglevel
* \--pidfile
* \--protocol
* \--region
* \--retries
* \--tag
* \--ha-connections

**说明**：*这些参数会附加到默认参数 `"no-autoupdate"`, `"metrics"` 和 `"loglevel"`。本地管理隧道会附加 `"origincert"` 和 `"config"`，远程管理隧道会附加 `"token"`，不能覆盖这些参数。*

**说明**：*如果参数需要路径，可使用 `/config` 作为根路径，可通过 VS Code 插件访问 `/addon_configs`。*

```yaml
run_parameters:
  - "--region=us"
  - "--protocol=http2"
  - "--loglevel=debug"
```

### 选项：`log_level`

控制插件日志输出级别，可根据需要调整详细程度。

**说明**：*如果要更改隧道本身日志级别，可使用 `run_parameters` 的 `--loglevel` 选项。*

```yaml
log_level: debug
```

可能值：

* `trace`：显示每个细节，包括所有内部函数调用。
* `debug`：显示详细调试信息。
* `info`：普通（通常）有用事件。
* `warning`：非错误的异常情况。
* `error`：运行时错误，不需要立即处理。
* `fatal`：严重错误，插件无法使用。

请注意，每个级别会自动包含更严重级别的日志信息，例如 `debug` 也会显示 `info` 消息。默认 `log_level` 为 `info`，推荐设置，除非正在排查问题。

## Home Assistant 配置

### configuration.yaml

由于 Home Assistant 会阻止代理/反向代理请求，你需要允许 Cloudflared 插件的请求。
插件在本地运行，因此 HA 必须信任 Docker 网络。
在 `/config/configuration.yaml` 中添加如下内容：

```yaml
http:
  use_x_forwarded_for: true
  trusted_proxies:
    - 172.30.33.0/24
```

**说明**：*这些 IP 范围默认不需要修改。*

**如果使用非标准 HA 部署（如 Proxmox），可能需要添加其他 IP/范围。尝试连接后查看 HA 日志以确定正确 IP。**

更改配置后，请重启 Home Assistant。

如需配置帮助，请参阅 \[高级配置教程]\[advancedconfiguration]。

## 插件 Wiki

更多高级 \[使用指南]\[how-tos] 和 \[故障排查]\[troubleshooting]，请访问 \[GitHub 插件 Wiki]\[addon-wiki]。

## 作者与贡献者

本仓库最初由 \[Tobias Brenner]\[tobias] 设置。

完整作者和贡献者列表，请查看 \[贡献者页面]\[contributors]。

## 许可协议

MIT 许可证

版权所有 (c) 2025 Tobias Brenner

特此免费授予任何获得本软件及相关文档文件（“软件”）副本的人无限制使用、复制、修改、合并、发布、分发、再授权和/或出售本软件的权利，并允许向其提供本软件的人在符合以下条件的情况下使用：

以上版权声明和本许可声明必须包含在本软件的所有副本或主要部分中。

本软件按“原样”提供，不附带任何形式的明示或暗示保证，包括但不限于适销性、特定用途适用性及不侵权保证。在任何情况下，作者或版权持有人均不对因软件或软件使用或其他交易产生的任何索赔、损害或其他责任负责，无论是合同、侵权或其他形式。

[addon-installation]: https://github.com/brenner-tobias/addon-cloudflared#installation
[addon-remote-tunnel]: https://github.com/brenner-tobias/addon-cloudflared/wiki/
