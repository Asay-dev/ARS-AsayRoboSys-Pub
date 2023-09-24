# ARS - AsayRoboSys 🤖
中文版点击 [这里](README_CN.md)

ARS is a Golang language robot development system that rapidly builds cross-platform robot software

*Click on "STAR ⭐" if you like*

Support Platform Support platform

|Name|Support|Info|
| :--- | :---: | :---: |
| Windows |✔ ️ | Total |
|Linux  | ✔ ️ | Total |
| MacOS | ✔ ️ | Total |
| Android | ✔ ️ | Total |
| STM32 | ✔ ️ | Serial |
| Arduino | ✔ ️ | Serial |

## Overview Function overview
- Message intermediate (zeromq) ❌
- GUI Window ARG-AsayRoboGui is Developing ❌
- Customize the message type
- Customize the sensor
- Serial Port tool
- socket server
- Logical node ❌
---
# ℹ ️ INFO
# # ✉ ️ Message
The -message class is used to build custom message types
- Adopt pipeline communication
- ZeroMQ service for message passing

# # 📟 Sensor
- Define your own sensor in the Sensor directory
- Bind the corresponding message type
- Define the corresponding service

# # 🍡 Serial
- Provides USB communication tools
TODO: UART I2C ...

# # 🛎 ️ Server
- Define your own sensor message server
- Start the sensor message server

---
# Usage
1. Download the function package, decompress it, and open it
2. `go mod tidy`
3. Write your own code in the corresponding directory
## message Defines the message
To define your own message type, see:
## sensor Build a sensor
Define your own sensor type, refer to 'pkg\sensor\tdsSensor.go', etc
## serial Serial port communication tool
Serial port tool can be invoked
## server Build message server
To define your own message server, see 'pkg\server\tds_sensor.go'

# Creation process
1. Create a message type under the /pkg/message directory
2. Create an object under the /pkg/sensor directory
3. Create a service under the /pkg/server directory and add a route to 'server/main'

The + inheritance comes from 'main' in each package

# Thank you
+ dependency package authors, thank you!