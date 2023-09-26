# ABROV参考文档

*每台机器根据客户要求不一样, 请参考自己的设备包含的部分*

**文档内容仅供技术参考, 可完整实现;  非本公司实际使用技术. 不要根据这个参考改装机器

+ [API接口文档](ARS-API.md)
+ [比赛说明书](比赛说明书参考.md)

# 使用场景描述

使用场景	场景描述
远程遥控	实现机器人的LTE网络下的遥控
水下运动	实现水下推进器运动
机械臂遥控	实现水下机械臂的遥控
开放接口	开放要求功能点的控制接口

# 总体架构

软件架构：
![](img/图片1.png)

硬件架构：
![](img/图片11.png)
网络结构:
![](img/5G架构图.drawio.png)
通信系统:
![](img/X220516%20ROV5G岸基系统示意图.png)
# 硬件
## Pixhawk 2.4.8 飞控
![](img/pix.png)
优势: 自带稳定算法, 提供官方上位机软件可以直接使用QGC软件控制, 可以自定义引脚的输出, 实时做出改变, 可以外接传感器 灯光 机械臂等外围硬件

## 树莓派

![](img/Pasted%20image%2020230926112442.png)

+ 上位机采用BCM2837, 用来作为STM32的信号中继和摄像头图像的推流
优势: 有板载网口方便作为信号的中继, 有板载GPIO方便开发连接下位机, 板载USB口可以直接安装摄像头, 读取摄像头数据
## MCU
![](img/Pasted%20image%2020230926112607.png)
+ 控制系统基于STM32F427单片机, 可以输出8个PWM信号, 控制整个机器人的6台推进器, 保证机器人的运动。协处理器使用STM32F100, 可以输出6个PWM信号, 控制ROV的灯光和机械臂的俯仰运动和抓取。

## 5G模块
![](img/5G基站.jpg)
优势: 自带天线和USB口, 可以直接插到树莓派上面进行使用, 提供LINUX驱动, 组网快捷方便, 插入5G卡使用
## 传感器单元
###  深度传感器MS5837
![](img/Pasted%20image%2020230926112650.png)
ELEC-DSI．3050内部传感器型号：TEMs5837·30BA50女兼容Ardusub.ELEC-DSI·3026内部传感器型号：TEMs5837·30BA26elec-dsl·3026的优点和区别：高化学耐久性和金属屏蔽，增强的结构和设计，材料允许在苛刻的液体介质环境中暴露，增强的化学耐久性。

## 运动控制单元
![](img/Pasted%20image%2020230926113034.png)
STM32F407使用PWM信号连接水下推进器的无刷电子调速器, 通过调整占空比, 控制推进器的转速, 从而使得ROV做出相应的运动姿态。水下推进器所使用无刷电子调速器为20A, PWM信号频率最高支持500HZ。下图为无刷电子调速器。

# 通信系统
1、通信方式
本系统中STM32F407和传感器单元采用IIC总线通信。
2、IIC协议
IIC通信过程由开始、结束、发送、响应、接收五个部分构成。
1) 开始信号和结束信号
开始信号：当SCL为高期间，SDA由高到低的跳变；
停止信号：当SCL为高期间，SDA由低到高的跳变；
![](img/Pastedimage20230926113648.png)
2) 数据传输
SDA的数据在SCL高电平期间被写入从机。所以SDA的数据变化要发生在SCL低电平期间。
3) 应答信号
一个字节按数据位从高位到低位的顺序传输完后，紧接着从设备将拉低SDA线，回传给主设备一个应答位(ACK)， 此时才认为一个字节真正的被传输完成。并不是所有的字节传输都必须有一个应答位，比如：当从设备不能再接收主设备发送的数据时，从设备将回传一个否定应答位(UACK)。
![](img/Pastedimage20230926113701.png)

4) 设备地址选取
I2C总线上的每一个设备都对应一个唯一的地址,主设备在传输有效数据之前要先指定从设备的地址，地址指定的过程和上面数据传输的过程一样，只不过大多数从设备的地址是7位的，然后协议规定再给地址添加一个最低位用来表示接下来数据传输的方向，0表示主设备向从设备写数据，1表示主设备向从设备读数据,每一小包数据由9位bit组成。

# 算法
## AI目标识别

