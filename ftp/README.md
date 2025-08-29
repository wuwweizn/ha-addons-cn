# Home Assistant 社区插件：FTP

[![版本][release-shield]][release] ![项目阶段][project-stage-shield] ![项目维护][maintenance-shield]

[![Discord][discord-shield]][discord] [![社区论坛][forum-shield]][forum]

[![通过 GitHub Sponsors 支持 Frenck][github-sponsors-shield]][github-sponsors]

[![通过 Patreon 支持 Frenck][patreon-shield]][patreon]

一个安全且高速的 Home Assistant FTP 服务器。

---

## 关于

FTP 协议有时仍然非常有用。虽然比较老旧，但仍有应用场景，例如大多数 IP 摄像头仍然支持通过 FTP 上传图片或视频。

此插件为 Hass.io 提供了一个相对安全的 FTP 服务器。虽然 FTP 本身（未加密）并不完全安全，但此插件支持 FTP over SSL（FTPS），并将虚拟用户限制（chroot）在其主目录中。

当然，如果你愿意，也可以使用此插件通过 FTP 访问你的 Home Assistant 配置文件。

---

[discord-shield]: https://img.shields.io/discord/478094546522079232.svg
[discord]: https://discord.me/hassioaddons
[forum-shield]: https://img.shields.io/badge/community-forum-brightgreen.svg
[forum]: https://community.home-assistant.io/t/home-assistant-community-add-on-ftp/36799?u=frenck
[github-sponsors-shield]: https://frenck.dev/wp-content/uploads/2019/12/github_sponsor.png
[github-sponsors]: https://github.com/sponsors/frenck
[maintenance-shield]: https://img.shields.io/maintenance/yes/2025.svg
[patreon-shield]: https://frenck.dev/wp-content/uploads/2019/12/patreon.png
[patreon]: https://www.patreon.com/frenck
[project-stage-shield]: https://img.shields.io/badge/project%20stage-production%20ready-brightgreen.svg
[release-shield]: https://img.shields.io/badge/version-v5.3.2-blue.svg
[release]: https://github.com/hassio-addons/addon-ftp/tree/v5.3.2
