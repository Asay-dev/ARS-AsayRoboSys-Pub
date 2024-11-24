# 开机配置

## 找到机器的IP
```
设备默认: 192.168.255.233
默认上位机: 192.168.255.234
```
1. 插路由器后台查看
2. 下载ip扫描器扫描: https://www.advanced-ip-scanner.com/cn/

## 下载软件

+ API版-QGC: http://qgroundcontrol.com/
+ 定制版: 询问客服定制软件界面

## 网络设置
进入网络设置, 确保处于专用网络模式, 确保防火墙关闭
![alt text](./img/image-3.png)

## 防火墙

1. **控制面板**然后选择**Windows Defender防火墙**. 如果您没有看到Windows Defender防火墙，请更改**查看由**选项到大或小的图标。

![brov2-firewall-setup-1](https://bluerobotics.com/wp-content/uploads/2016/06/brov2-firewall-setup-1.png)

2. 选择“允许应用程序或功能通过Windows Defender防火墙”.

![brov2-firewall-setup-2](https://bluerobotics.com/wp-content/uploads/2016/06/brov2-firewall-setup-2.png)

2. 选择**更改设置**，在应用列表中找到“QGroundControl开发团队提供的开源地面控制应用程序”或“QGroundControl”。旁边的框中选中后点OK.

![brov2-firewall-setup-3](https://bluerobotics.com/wp-content/uploads/2016/06/brov2-firewall-setup-3.png)

# 手柄遥控

+ 开启手柄

![alt text](./img/image.png)

![alt text](./img/image-1.png)

1. 手柄选项, 开启手柄打钩

2. 手柄说明, 操作需要先解锁电机

![手柄说明](./img/手柄.drawio.png)

# QGC说明
![alt text](./img/image-2.png)

+ Manual - 手动模式允许操作员直接控制航行器的推进器，没有任何自动稳定或自动控制干预。

+ Stabilize - 稳定模式会自动保持航行器的水平姿态。在这个模式下，如果操作员释放控制杆，航行器会自动恢复水平位置。

+ Acro - 特技模式，提供了高级的机动性能和控制灵敏度，适用于经验丰富的操作员。在这个模式下，航行器的响应更加敏感和迅速。

+ Depth Hold - 深度保持模式允许航行器在水平方向上自由移动，同时自动保持当前水深，不上浮也不下沉。

+ Auto - 自动模式根据预设的任务或路径进行自动航行。操作员设定好路线后，航行器会自动执行。

+ Guided - 导引模式允许操作员通过指定具体的目标点或路径来远程控制航行器，通常用于复杂或精确的操作。

+ Circle - 圆周模式使航行器围绕一个指定的GPS坐标或目标物自动旋转。

+ Position Hold - 位置保持模式使航行器保持在一个固定的位置和姿态，即使在水流或其它外力的影响下也能保持不动。

每种模式都有其特定的用途和优点，适用于不同的操作需求和环境条件。选择合适的模式可以提高操作效率和安全性。