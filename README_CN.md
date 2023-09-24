# ARS - AsayRoboSys 🤖

ARS是一个Golang语言的机器人开发系统，快速构建跨平台的机器人软件

**喜欢使用的话点个 STAR ⭐**

支持平台 Support Platform

|Name|Support|Info|
|:---|:---:|:---:|
|Windows|✔️|Total|
|Linux|✔️|Total|
|MacOS|✔️|Total|
|Android|✔️|Total|
|STM32|✔️|Serial|
|Arduino|✔️|Serial|

## Overview 功能概览
- 消息中间间（zeromq）❌
- GUI窗口 ARG-AsayRoboGui 开发中 ❌
- 自定义消息类型 
- 自定义传感器
- 串口工具
- socket服务器
- 逻辑节点 ❌
---
# ℹ️INFO
## ✉️Message
- message 类用于构建自定义的消息类型
- 采用管道通信
- ZeroMQ服务来进行消息传递

## 📟Sensor
- 在sensor目录定义自己的传感器
- 绑定对应的消息类型
- 定义对应的服务

## 🍡Serial
- 提供USB通信工具
TODO: UART I2C ...

## 🛎️Server
- 定义自己的传感器消息服务器
- 启动sensor消息服务器

---
# Usage
1. 下载本功能包并解压打开
2. `go mod tidy`
3. 在对应目录编写自己的代码
## message 定义消息
定义自己的消息类型，参考:
## sensor 构建传感器
定义自己的传感器类型，参考`pkg\sensor\tdsSensor.go`等
## serial 提供串口通信工具
可调用串口工具
## server 构建消息服务器
定义自己的消息服务器，参考`pkg\server\tds_sensor.go`

# 创建过程
1. /pkg/message目录下面创建消息类型
2. /pkg/sensor目录下面创建对象
3. /pkg/server目录下面创建服务, `server/main`当中添加路由

+ 继承均来自每个包的 `main`

# 感谢
+ 依赖包的作者，谢谢您们！