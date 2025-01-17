---
BADGE-NPM version: https://img.shields.io/npm/v/iobroker.wiegand-tcpip.svg
BADGE-Downloads: https://img.shields.io/npm/dm/iobroker.wiegand-tcpip.svg
BADGE-Number of Installations: https://iobroker.live/badges/wiegand-tcpip-installed.svg
BADGE-Current version in stable repository: https://iobroker.live/badges/wiegand-tcpip-stable.svg
BADGE-Dependency Status: https://img.shields.io/david/kbrausew/iobroker.wiegand-tcpip.svg
BADGE-NPM: https://nodei.co/npm/iobroker.wiegand-tcpip.png?downloads=true
translatedFrom: en
translatedWarning: 如果您想编辑此文档，请删除“translatedFrom”字段，否则此文档将再次自动翻译
editLink: https://github.com/ioBroker/ioBroker.docs/edit/master/docs/zh-cn/adapterref/iobroker.wiegand-tcpip/README.md
title: **设置**
hash: dfVQu1onk5GZrjjfwS/zm9lJvc7qy6w2j6crpfH8rgY=
---
＃ **设置**
- [初始启动](#initial-start-up) 首次访问设备
- [设置适配器](#door-access-controllers-settings) 设置 ioBroker 适配器
  - [TCP/IP 网络设置](#tcpip-network-settings) 设置适配器网络
  - [控制器设置](#controllers-settings) 设备设置
    - [广播](#broadcast)
      - [序列号](#serial-number)
    - [专用网络设置](#dedicated-network-setup)
      - [序列号](#serial-number)
      - [设备网络地址](#device-network-address)
      - [暴露服务器主机地址](#exposed-server-host-address)
      - [暴露服务器主机端口](#exposed-server-host-port)

## **初始启动**
首次连接设备时，输入网络数据可能很有用。

这些步骤是可选的，只有在 ioBroker 实例的本地网络之外的另一个远程网络上使用设备时才需要

* 去做这个...
  - 将设备连接到 ioBroker 所在的同一网络。没有 Docker、VPN 或其他子网。 [^1]
  - 使用默认设置安装并启动适配器。
  - 进入配置并切换到“设备远程设置”选项卡
  - 运行设备扫描。

![按钮设备扫描](../../../en/adapterref/iobroker.wiegand-tcpip/images/device-scan.png) 有两种可能的错误消息会导致找不到设备[^3]、[^4]

  - 如果您有多个设备处于活动状态，请在“设备 ID”下拉框中选择您想要的设备。
  - 将所需的地址数据放入适当的输入字段[^2]
  - 现在在目标网络中安装设备

## **门禁控制器设置**
### **TCP/IP 网络设置**
#### **网络接口**
从列表中，选择您已将设备连接到的网络主机适配器。 [^2]

- 特殊地址
  - `0.0.0.0` 所有可用接口（默认）
  - `127.0.0.1` 仅限本地主机网络（适用于 [模拟器](https://github.com/uhpoted/uhpote-simulator)）
  - 如果您知道自己想要什么，则可以使用所有其他人。例如VPN，码头工人等...

#### **发件人端口**
默认值为 60000。如果没有来自网络的错误消息，则无需进行更改。

#### **接收器端口**
默认值为 60001。如果没有来自网络的错误消息，则无需进行更改。
我为适配器重新定义了端口 60099。如果某些东西不起作用，请将其更改回默认值。

#### **连接超时以毫秒为单位**
默认值为 2500（2.5 秒）。
通过网络进行任何通信的超时。
未经协商请勿更改。
1000以下和10000以上的数值暂时可以工作，但在实际操作中总是会导致错误。

#### **心跳间隔以毫秒为单位**
默认值为 300000（300 秒 == 5 分钟）。
两次尝试建立与设备的标准连接以决定它是否处于活动状态之间的时间。
低于 60000 和高于 900000 的值会导致难以分析的不良副作用。

#### **以毫秒为单位的最大时间偏差**
默认值为 60000（60 秒 == 1 分钟）最大时间偏差（以毫秒为单位）。
如果偏差较大，则重新校准控制器时钟。
低于 1200 毫秒的值将被忽略并关闭校准。

#### **低级调试**
默认关闭。如果启用，原始网络通信将记录到调试日志中。
没有开发人员的要求，无需更改。

### **控制器设置**
通过网络设置正向和反向通道的设备。
每个可用设备使用 **+ / add** 和 **trash**。
主机 (ioBroker) 和设备之间的通信有两种选择。
有限广播和专用网络设置（单播和定向广播）。 [^7]

＃＃＃＃ **序列号**
您设备的序列号。

#### **型号类型**
输入门模型

#### **有限广播** [^7]
仅添加序列号和型号类型，不添加其他地址/网络数据。
>在这种情况下，所有组件必须在同一个子网中。
>这包括发送方（控制器）和接收方（ioBroker）。
>这可以通过两个组件上的相同网关地址和网络掩码来识别。

>在所有其他情况下，始终使用“专用网络设置”。

#### **专用网络设置（单播和定向广播）** [^7]
请输入所有地址数据...

#### **设备网络地址** [^7]
远程网络上设备的公开 IP 地址（单播）。 [^2] [^8]

#### **暴露的服务器主机地址** [^7]
ioBroker 实例在远程网络上的公开 IP 地址（单播）。 [^2] [^8]

#### **暴露的服务器主机端口** [^7]
在 NAT [^5] 和 Docker-Exposed [^6] 之后，远程网络上 ioBroker 实例的公知 IP 端口。

[^1]: If you are unable to connect the device to the same local network as the ioBroker instance,

  您必须以另一种替代方式设置 IP 地址

[^2]: The device only allows IPv4 addresses.

[^3]: ![Error message: No Device found](../../../en/adapterref/iobroker.wiegand-tcpip/images/no-devices-found.png)

[^4]: ![Error message: Adapter not started](../../../en/adapterref/iobroker.wiegand-tcpip/images/adapter-not-run.png)

[^5]: [NAT RFC#2663](https://datatracker.ietf.org/doc/html/rfc2663)

[^6]: [Docker CLI: Port](https://docs.docker.com/engine/reference/commandline/port/)

[^7]: ![Network Setup](../../../en/adapterref/iobroker.wiegand-tcpip/images/network-setup.png)

[^8]: You can replace the "Unicast Address" with the "Directed Broadcast Address" in the configuration.

## Changelog
[Changelog](CHANGELOG.md)

## License
GPL-3.0-only