# ABROV参考文档

*每台机器根据客户要求不一样, 请参考自己的设备包含的部分*

**文档内容仅供技术参考, 可完整实现;  非本公司实际使用技术. 不要根据这个参考改装机器

+ [API接口文档](ARS-API.md)
+ [比赛说明书](比赛说明书参考.md)

# 开机配置
## 找到机器的IP
1. 插路由器后台查看
2. 下载ip扫描器扫描: https://www.advanced-ip-scanner.com/cn/

## 下载软件
+ API版-QGC: http://qgroundcontrol.com/
+ 定制版: 询问客服定制软件界面

## 网络设置

1. 窗口**控制面板**选择**网络与共享中心**. 如果您没有看到“网络和共享中心”，请将“**查看由**选项到大或小的图标。

![brov2-windows-network-setup-1](https://bluerobotics.com/wp-content/uploads/2016/06/brov2-windows-network-setup-1.png)

2. 在“网络和共享中心”窗口中，选择**更改适配器设置**.

![brov2-windows-network-setup-2](https://bluerobotics.com/wp-content/uploads/2016/06/brov2-windows-network-setup-2.png)

3. 以太网适配器，右键单击此以太网适配器，然后选择**属性**.

![brov2-windows-network-setup-3](https://bluerobotics.com/wp-content/uploads/2016/06/brov2-windows-network-setup-3.png)

4. 在属性对话框中，点击**互联网协议版本4（TCP/IPv4）**来突出显示它，然后点击**属性**.

![brov2-windows-network-setup-4](https://bluerobotics.com/wp-content/uploads/2016/06/brov2-windows-network-setup-4.png)

5. 选择使用以下IP地址**192.168.2.1**为IP地址和**255.255.255.0**子网掩码。选择OK，然后您可以关闭其余的窗口。

![brov2-windows-network-setup-5](https://bluerobotics.com/wp-content/uploads/2016/06/brov2-windows-network-setup-5.png)

## 防火墙

1. **控制面板**然后选择**Windows Defender防火墙**. 如果您没有看到Windows Defender防火墙，请更改**查看由**选项到大或小的图标。

![brov2-firewall-setup-1](https://bluerobotics.com/wp-content/uploads/2016/06/brov2-firewall-setup-1.png)

2. 选择“允许应用程序或功能通过Windows Defender防火墙”.

![brov2-firewall-setup-2](https://bluerobotics.com/wp-content/uploads/2016/06/brov2-firewall-setup-2.png)

2. 选择**更改设置**，在应用列表中找到“QGroundControl开发团队提供的开源地面控制应用程序”或“QGroundControl”。旁边的框中选中后点OK.

![brov2-firewall-setup-3](https://bluerobotics.com/wp-content/uploads/2016/06/brov2-firewall-setup-3.png)



## API版本和定制机器 ssh连接机器
1. 下载ssh工具: https://mobaxterm.mobatek.net/
2. 连接到上面查找到的IP
3. 账号密码问客服

### 启动服务

1. 编辑 `config` 文件, 将 `client_address` 设置为上位机的 ip 地址
2. `sudo ./ARS` 启动(版本不同名字不同 `ls` 查看)

# 使用场景描述

使用场景	场景描述
远程遥控	实现机器人的LTE网络下的遥控
水下运动	实现水下推进器运动
机械臂遥控	实现水下机械臂的遥控
开放接口	开放要求功能点的控制接口

# 总体架构

硬件架构(接线图):

![MOS电源管理架构图](E:\01WorkSpace\asayBROV-CTF\架构图\MOS电源管理架构图.png)

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

