# Home Assistant 插件：文件编辑器（File editor）

## 安装

按照以下步骤在系统中安装此插件：

1. 在 Home Assistant 前端导航到 **设置** -> **插件** -> **插件商店**。
2. 找到 “File editor” 插件并点击它。
3. 点击 “安装（INSTALL）” 按钮。

## 使用方法

通常，此插件无需你进行额外配置。

1. 切换 “在侧边栏显示（Show in sidebar）” 选项，将文件编辑器添加到主菜单。
2. 启动插件。
3. 刷新浏览器，侧边栏中现在可见 “File editor”。
4. 点击侧边栏菜单中的 “File editor” 开始配置文件！

## 配置

插件配置示例：

```yaml
dirsfirst: false
enforce_basepath: false
git: true
ignore_pattern:
  - __pycache__
ssh_keys: []
```

### 选项：`dirsfirst`（必需）

此选项允许在文件浏览器树中将目录列在文件前面。

* 设置为 `true`：目录优先显示
* 设置为 `false`：按默认顺序显示

### 选项：`enforce_basepath`（必需）

* 设置为 `true`：访问仅限 `/homeassistant` 目录（Home Assistant 内部的 `/config` 文件夹）。

### 选项：`git`（必需）

* 设置为 `true`：插件会为支持 Git 的目录初始化 Git。

### 选项：`ignore_pattern`（必需）

此选项允许在文件浏览器树中隐藏特定文件或文件夹。
默认情况下，会隐藏 `__pycache__` 文件夹。

### 选项：`ssh_keys`（必需）

包含 SSH 私钥的文件名列表，用于访问远程 Git 仓库。

## 已知问题与限制

* 此插件只能通过 Ingress 使用，无法直接访问文件系统。

## 支持

遇到问题？你有多种途径获取帮助：

* [Home Assistant Discord 聊天服务器][discord]
* Home Assistant [社区论坛][forum]
* 访问 [Reddit 子版块][reddit]：[/r/homeassistant][reddit]

如果发现插件有 bug，请 [在 GitHub 上提交 issue][issue]。

[discord]: https://discord.gg/c5DvZ4e
[forum]: https://community.home-assistant.io
[issue]: https://github.com/home-assistant/addons/issues
[reddit]: https://reddit.com/r/homeassistant
