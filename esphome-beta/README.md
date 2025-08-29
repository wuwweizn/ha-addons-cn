# ESPHome 设备构建器 Beta

[![ESPHome logo][logo]][website]

[![GitHub stars][github-stars-shield]][repository]
[![Discord][discord-shield]][discord]

## 关于

这个插件允许你直接通过 Home Assistant 编写配置，将微控制器转换为智能家居设备，**无需任何编程经验**。
你只需编写 YAML 配置文件，其余的（OTA 更新、固件编译等）都由 ESPHome 处理。

<p align="center">
<img title="ESPHome Device Builder 截图" src="https://github.com/esphome/home-assistant-addon/raw/main/esphome-beta/images/screenshot.png" width="700px"></img>
</p>  

[查看 ESPHome 文档][website]

## 示例

使用 ESPHome，你可以从几行 YAML 直接生成定制固件。例如，要添加一个 [DHT22][dht22] 温湿度传感器，只需在配置文件中写 8 行 YAML：

<img title="ESPHome DHT 配置示例" src="https://github.com/esphome/home-assistant-addon/raw/main/esphome-beta/images/dht-example.png" width="500px"></img>

然后点击 **UPLOAD**，传感器就会神奇地出现在 Home Assistant 中：

<img title="ESPHome Home Assistant 自动发现" src="https://github.com/esphome/home-assistant-addon/raw/main/esphome-beta/images/temperature-humidity.png" width="600px"></img>

[discord]: https://discord.gg/KhAMKrd
[repository]: https://github.com/esphome/esphome
[discord-shield]: https://img.shields.io/discord/429907082951524364.svg
[github-stars-shield]: https://img.shields.io/github/stars/esphome/esphome.svg?style=social&label=Star&maxAge=2592000
[dht22]: https://beta.esphome.io/components/sensor/dht.html
[releases]: https://beta.esphome.io/changelog/index.html
[logo]: https://github.com/esphome/home-assistant-addon/raw/main/esphome-beta/logo.png
[website]: https://beta.esphome.io/
