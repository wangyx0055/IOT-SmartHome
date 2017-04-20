# E居—智能家居系统

<a href="#English">English</a> <a href="#chinese">简体中文</a>

[Instruction](https://github.com/lhtdeg/IOT-SmartHome/wiki) [项目说明](https://github.com/lhtdeg/IOT-SmartHome/wiki/%E9%A6%96%E9%A1%B5) 

<a href="#demo">Demo</a>

## <p id="chinese">主要特点</p>

- 基于MQTT协议
- 硬件基于Arduino，方便开发
- 可以接入iOS的HomeKit，使用Siri控制电器（HomeBridge实现）
- 可单一节点运行（ESP8266实现）
- 与外网断开连接时可控制（Zigbee实现）
- 直观的WEB页面展示
- 可接入第三方平台（OneNET、机智云）
- Android APP采用Material Design风格
- 网关与服务端可以部署在Windows、Linux、macOS及树莓派平台
- 最小系统成本在10元左右（使用ESP8266）

## 安全性

如果对安全性有要求，请尽可能使用Zigbee+网关的模式，不要使用ESP8266直接连入网络，因为Arduino的MQTT Client不支持TLS。

## 支持外接MCU

ESP8266或Zigbee的开发板一般接口较少，并且大部分都是GPIO。对于有特殊需求的用户，可以采取ESP8266/Zigbee节点+MCU的方式。在这种方式中，ESP8266或Zigbee节点通过串口传输命令，MCU负责将命令解析并执行。

## 待添加功能

- 使用Tensorflow学习用户习惯
- 利用kafka分发事件
- RTMP直播流服务器
- iOS APP开发
- Android端语音控制支持

## 视频展示

`此处有视频`

# <p id="English">EHome SmartHome with Arduino and MQTT</p>

## License

```
Copyright 2016 Hatim Liu

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

