# 配置（Configuration）

![image](https://raw.githubusercontent.com/adamoutler/HassOSArgonOneAddon/main/gitResources/Configuration.png)

## 摄氏或华氏

选择使用摄氏度（Celsius）或华氏度（Fahrenheit）。

CorF – 设置使用摄氏或华氏温度单位。

## 温度范围（Temperature Ranges）

![image](https://raw.githubusercontent.com/adamoutler/HassOSArgonOneAddon/main/gitResources/FanRangeExplaination.png)

请合理设置风扇的温度区间。

- **LowRange** 最低温度阈值。
当温度达到这个值时，风扇会以 33% 转速运行。
低于这个温度时，风扇会关闭。
- **MediumRange** 作为 33% 和 66% 转速之间的分界温度
- **HighRange** 达到此温度时，风扇将以 100% 全速运行。
这是最高温度阈值。

## 启用 I2C

要启用 I2C，必须使用以下方法之一：

### 简单方法
安装 HassOS I2C Configurator 插件。
[Addon](https://community.home-assistant.io/t/add-on-hassos-i2c-configurator/264167)

### 官方方法
按照 Home Assistant 官方 Raspberry Pi 安装指南中的 I2C 启用步骤操作。
[Official Guide](https://www.home-assistant.io/installation/raspberrypi/#enable-i2c)

## 支持

需要帮助？请前往社区链接。 [here](https://community.home-assistant.io/t/argon-one-active-cooling-addon/262598/8).

请尽量详细描述问题。

如果无法详细描述……那就尽量夸张一点表达
