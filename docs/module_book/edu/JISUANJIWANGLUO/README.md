# 《计算机网络7》

<img src='./IMG_6258.jpg'/>

## 书评

上课只讲授前6章节，分别是一章概述加五层模型。

课设是 编程实现 网络层 程序（ping arp icmp 之类），当时语言选择是 Java 和 C++，时至今日仍深刻记得 Java 编写网络层压力之大，后来是用 C++ 手动封（IP | ICMP）包，调用 Winsocket 实现。

面试来说，个人感觉偏重第五章内容（运输层 TCP | UDP，三次握手？可靠 UDP 实现？）。

## 第 1 章 概述

### 1.3.2 互联网的核心部分

- **电路交换**——整个报文的比特流连续地从源点直达终点，好像在一个管道中传送。
- **报文交换**——整个报文先传送到相邻结点，全部存储下来后查找转发表，转发到下一个结点。（现在报文交换已不再使用了）
- **分组交换**——单个分组（这只是整个报文的一部分）传送到相邻结点，存储下来后查找转发表，转发到下一个结点。

### 1.6 计算机网络的性能

- 速率
- 带宽
- 吞吐量
- 时延（发送时延，传播时延，处理时延，排队时延）
- 时延带积宽
- 往返时间 RTT
- 利用率

TCP/IP 就常被称为是事实上的国际标准。

### 1 应用层
应用层交互的数据单元称为**报文**（message）。
### 2 运输层
运输层的任务就是负责向两台主机中**进程**之间的通信提供通用的数据传输服务。（TCP UDP）

- **传输控制协议 TCP（Transmission Control Protocol）**——提供面向连接的、可靠的数据传输服务，其数据传输的单位是**报文段**（segment）。
- **用户数据报协议 UDP（User Datagram Protocol）**——提供无连接的、尽最大努力（best-offort）的数据传输服务（不保证数据传输的可靠性）。其数据传输的单位是**用户数据报**。
### 3 网络层
网络层为**主机**之间提供逻辑通信。

**IP 数据报**
### 4 数据链路层
在两个相邻结点之间传送数据，**帧**（frame）。
### 5 物理层
物理层传输的单位是**比特**。


## 第 2 章 物理层

### 2.4 信道复用技术
- **频分复用 FDM（Frequency Division Multiplexing）**：频分复用的所有用户在同样的时间占用不同的带宽资源。
- **时分复用 TDM（Time Division Multiplexing）**：时分复用的所有用户在不同的时间占用同样的频带宽度。
- **统计时分复用 STDM（Statistic TDM）**：改进的时分复用。
- **波分复用 WDM（Wavelength Division Multiplexing）**
- **码分复用 码分多址 CDMA（Code Division Multiple Access）**

### 2.6 ADSL 技术
非对称数字用户线 ADSL（Asymmetric Digital Subscriber Line）技术是用数字技术对现有的模拟电话用户线进行改造。

我国目前采用的方案是**离散多音调 DMT（Discrete Multi-Tone）调制技术**

## 第 3 章 数据链路层
- **链路（link）**就是从一个结点到相邻结点的一段物理线路。（物理链路）
- **数据链路（data link）**：物理链路加上必要的通信协议。（逻辑链路）

数据链路协议三个基本问题：

- **封装成帧（framing）**：每一种链路层协议都规定了所能传送的帧的**数据部分长度上限——最大传送单元 MTU**（Maximum Transfer Unit）。
- **透明传输**：不管从键盘上输入什么字符都可以放在这样的帧中传输过去。（字节填充法）
- **差错控制**：误码率 BER（Bit Error Rate）循环冗余检验 CRC（Cyclic Redundancy Check）（或会出现帧丢失、帧重复、帧失序）

数据链路层可以不向网络层提供 “可靠传输” 服务。

### 3.2 点对点协议 PPP

## 第 4 章 网络层

网际协议 IP 是 TCP/IP 体系中两个最主要的协议之一，也是最重要的互联网标准之一。

与 IP 协议配套使用的还有三个协议：

- **地址解析协议 ARP（Address Resolution Protocol）**
- **网际控制报文协议 ICMP（Internet Control Message Protocol）**
- **网际组管理协议 IGMP（Internet Group Management Protocol）**

根据中间设备所在的层次，可以有以下四种不同的中间设备：

- 物理层使用的中间设备叫做**转发器（repeater）**。
- 数据链路层使用的中间设备叫做**网桥**或**桥接器（bridge）**。
- 网络层使用的中间设备叫做**路由器（router）**。
- 在网络层以上使用的中间设备叫做**网关（gateway）**。

### 4.2.5 IP 数据报的格式

### ICMP

## 第 5 章 运输层

当运输层**采用面向连接的 TCP 协议时，尽管下面的网络是不可靠的**（只提供尽最大努力服务），但这种逻辑通信信道就相当于**一条全双工的可靠信道**。但当运输层采用**无连接的 UDP 协议**时，这种逻辑通信信道仍然是一条**不可靠信道**。

### 5.1.2 运输层的两个主要协议

使用 UDP 和 TCP 协议的各种应用和应用层协议：

| 应用 | 应用层协议 | 运输层协议 |
| - | - | :-: |
| 名字转换 | DNS（域名系统） | UDP |
| 文件传送 | TFTP（简单文件传送协议） | UDP |
| 路由选择协议 | RIP（路由信息协议） | UDP |
| IP 地址配置 | DHCP（动态主机配置协议） | UDP |
| 网络管理 | SNMP（简单网络管理协议） | UDP |
| 远程文件服务器 | NFS（网络文件系统） | UDP |
| IP 电话 | 专业协议 | UDP |
| 流式多媒体通信 | 专用协议 | UDP |
| 多播 | IGMP（网际组管理协议） | UDP |
| 电子邮件 | SMTP（简单邮件传送协议） | TCP |
| 远程终端接入 | TELNET（远程终端协议） | TCP |
| 万维网 | HTTP（超文本传送协议） | TCP |
| 文件传送 | FTP（文件传送协议） | TCP |

### // 5.2 用户数据报协议 UDP

### 5.3 传输控制协议 TCP 概述

1. TCP 是面向连接的运输层协议
2. 每一条 TCP 连接只能有两个端点（endpoint）
3. TCP 提供可靠交付的服务
4. TCP 提供全双工通信
5. 面向字节流

套接字 socket = （IP 地址：端口号）

TCP 连接 ::= {socket1, socket2} = {（IP1，port1），（IP2，port2）}

### 5.4 可靠传输的工作原理

停止等待协议

连续 ARQ 协议

### // 5.5 TCP 报文段的首部格式

### 5.6 TCP 可靠传输的实现

### 5.7 TCP 的流量控制

### 5.8 TCP 的拥塞控制

慢开始、拥塞避免、快重传、快恢复

### ★5.9 TCP 的运输连接管理

## 第 6 章 应用层

## // 第 7 章 网络完全

## // 第 8 章 互联网上的音频/视频服务

## // 第 9 章 无线网络和移动网络