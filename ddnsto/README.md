好的，我帮你写一个完整的 `README.md` 示例，针对你的 **DDNSTO HA Add-on** 项目，风格清晰、易读，并涵盖安装、配置和使用说明：

```markdown
# DDNSTO Home Assistant Add-on

![Panel Icon](https://img.icons8.com/material/48/000000/domain.png)

DDNSTO 动态域名解析服务集成，用于自动更新公网 IP 到 DDNSTO 平台，支持 Home Assistant 使用。

---

## ?? 版本

**当前版本:** 3.5.0  
**兼容架构:** `amd64`, `aarch64`  
**镜像地址:** `ghcr.io/wuwweizn/ddnsto:3.5.0`  

---

## ?? 功能

- 自动同步公网 IP 到 DDNSTO  
- 支持 Home Assistant 面板访问和管理  
- 多架构支持：amd64 / aarch64  

---

## ?? 安装

### 通过 GitHub 仓库安装

1. 在 Home Assistant UI 中，进入 **设置 → 加载项商店 → 添加自定义仓库**  
2. 仓库地址填：  
```

[https://github.com/wuwweizn/wwzn-china](https://github.com/wuwweizn/wwzn-china)

````
3. 点击 “添加” 后搜索 `ddnsto`，安装即可  

### 镜像安装（高级）

直接在 HA Add-on 配置中使用镜像：
```yaml
image: "ghcr.io/wuwweizn/ddnsto:3.5.0"
````

---

## ?? 配置

在 Add-on 配置页面填写：

```yaml
token: "你的 DDNSTO Token"
```

> `token` 是你在 DDNSTO 平台获取的授权码，用于更新域名解析。

---

## ?? 使用说明

1. 启动 Add-on
2. Add-on 会自动使用 `token` 更新公网 IP
3. 可通过 Home Assistant 面板查看状态

---

## ?? 高级功能

* 支持 `host_network: true`，保证 IP 更新准确
* 支持后台服务启动 (`boot: manual`)
* 面板图标 `mdi:application-variable`

---

## ?? 注意事项

* 确保 GHCR 镜像已存在并推送多架构 manifest
* HA 版本需支持 `image` 字段拉远程镜像

---

## ?? 链接

* [GitHub 仓库](https://github.com/wuwweizn/wwzn-china)
* [DDNSTO 官方网站](https://www.ddnsto.com/)

---


