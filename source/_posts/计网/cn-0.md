---
title: 计网总复习
date: 2020-08-11T10:30:00+08:00
categories: 计算机网络
---

|TCP/IP|OSI|数据单元|主体|协议|
|---|---|---|---|---|
||应用层|报文 message|进程|SMTP|
|应用层 Application|表示层 Presentation|
||会话层 Session|
|传输层 Transport||分段 segment|端口|TCP UDP|
|网络层 Network||分组/数据包 packet|主机|IP|
|链路层 Data Link||帧 frame|节点|以太|
|物理层 Physical|

socket：
- 相当于操作系统的 API 罢了
- [UDP socket 教程](https://www.jianshu.com/p/054fe6632bee)

# 1 计算机网络与因特网

按范围分类
- Body Area Network
- Personal Area Network
- Metropolitan Area Network
- Wide Area Network
- InterPlanetary Network

按节点移动性分类
- The Internet
- Wireless Sensor Network
- Optical Network
- Mobile Communication System
- Satellite Communication Network
- Mobile Ad hoc Network

## 1.3 网络核心

### 分组交换

分组交换中不会预留带宽、缓存等

计算机网络是分组交换

### 电路交换

电路交换中会预留带宽和缓存，建立连接时，沿途所有交换机都为其维护连接

电话网络是电路交换

电路交换的优势是可确保服务质量，有专用资源，不会被干扰

## 1.4 分组交换网中的时延、丢包和吞吐量

### 端到端时延

$$d_{end-end} = N (d_{proc} + d_{trans} + d_{prop})$$

传播延时 prop只与链路长度有关，视为常量

- 消息 message：应用层中进程间交互的数据单元
- 分段 segment：传输层中端口间交互的数据单元
- 分组 packet：网络层中主机间交互的数据单元
- 帧 frame：数据链路层中节点间交互的数据单元

# 2 应用层

|应用|应用层协议|传输层协议|
|---|---|---|
|Email|SMTP/POP3|TCP
|The Web|HTTP|TCP
|File transfer|FTP|TCP
|Resolve domain names|DNS|UDP
|Trivial File Transfer|TFTP|UDP
|Remote login|Telnet|TCP

get 返回信息中的 content length 单位是字节

邮箱服务器之间使用 SMTP

# 3 传输层

## UDP（User Datagram Protocol）

几乎等同裸的 IP，只能通过网络层（IP）提供的源地址信息分辨发送者

- 无连接传输，不可靠，可靠性要由应用层实现
- 首部 8 字节，总长不超过 64KB（$2^{16}$）
- 服务端一个套接字可接收多个客户端连接

![](/2020/04/09/计网/cn-3/udp.png)

### 校验

（每个字长 16 bit）

对包含伪首部、首部、数据在内的数据：
1. 每 16 位求和得到一个 32 位数
2. 若高 16 位不为 0，则高 16 位与低 16 位相加，得到新的 32 位数
3. 重复步骤 2 直到高 16 位为 0，将低 16 位 **取反** 得到校验和

> **取反**使得检验时只要将校验码和数据**一起相加**即可得到**全1**

能确保检测到 1bit 错误，2bit 及以上不一定能检测。

> 伪首部包含 源IP，目的IP，补位用的8位全0，协议代码（17），UDP数据包长度。伪首部仅用于计算校验和，不会真的发送。

## TCP（Transmission Control Protocol）

- 可靠传输，有持续连接和非持续两种
- 首部 20~24 字节
- 服务端一个套接字仅服务一个客户端连接

### Reliable Data Transfer

参考：[可靠数据传输基本原理](https://blog.csdn.net/zy010101/article/details/88981728)

rdt 是没有窗口的

1. rdt1.0：
   - 假设信道完全可靠
   - 收发双方都只有一个状态
2. rdt2.0 **停等**：
   - 假设信道只可能比特受损
   - 差错检测，接收方反馈，重传：NAK 的时候重传，ACK 的时候继续
   - 不能在等待反馈的时候接收上层数据，故称 **停等**
3. rdt2.1：
   - 考虑反馈受损
   - 加上分组编号，由于停等，故只要 0 1 两个编号
4. rdt 3.0 **ABP，比特交换协议**：
   - 考虑数据丢失
   - 加入定时器 RTT（往返时间 round trip time），超时就重传
   - 利用率：$U_{sender}=\frac{L/R}{RTT+L/R}$

### Go Back N

- 发送方可以有 N 个未确认的数据包（也就是最多能 回退 N）
- 接收方只依次 ACK，不能跳跃。若收到的包不连续，则持续 ACK 上一个连续的包
- 计时器给最老的、未确认的包计时
- 刚建立连接时，接收方构造一个虚的 *上次确认*
- $N=2^k$，k 为数据包序号长度

### Selective Repeat

- 发送方可以有 N 个未确认的数据包
- 接收方为每个数据包单独 ACK
- 每个数据包都有一个计时器
- $N{\leq}2^{k-1}$，否则若 ACK 全丢失，会把重传数据当成新数据

### TCP

是 GBN 和 SR 的结合
- 像 GBN 一样只为最老的数据包计时
- 像 SR 一样支持不连续的ACK，即：支持累积确认，总是传 ACK 请求的包

![](/2020/04/09/%E8%AE%A1%E7%BD%91/cn-3/tcp-header.jpg)

#### ACK

确认的 ACK = 发送的 seq+1；确认的 SEQ = 发送的 ack。双方都是这样

序列号是当前字节在文件中的偏移量，确认号是希望收到的下一个字节的偏移量

![](/2020/04/09/%E8%AE%A1%E7%BD%91/cn-3/tcp-example.jpg)

> 只有 TCP 的 ACK 会超前，GBN、SR 的ACK 都不超前

#### RTT

计时器要长于 RTT
- 过短：不必要的重传
- 过长：效率低

估计 RTT：
- SampleRTT：忽略重传的，并且最近的传输权重大

> 忽略重传：是因为若出现 premature timeout，即第一次的 ACK 在超时重传后才送达，则发送方的 RTT 测量为错误结果

#### 重传

三种重传：
1. 超时重传：定时器结束时未收到 ACK，则重传
2. premature timeout：重传后收到 ACK，接收方收到重传后仍确认最大的序号
3. 跳过 ACK：没收到上一个 ACK，就收到了后面的 ACK，发送方仍继续发送收到的 ACK 请求的数据包

总之一切照常

**快速重传**：连续收到三个相同的 ACK 就立刻重传，不管定时器

#### 流量控制

发送方有一个接收窗口 rwnd，即未确认的数据包不能多于 rwnd。也就是 GBN 和 SR 里的 N。

#### 三次握手

![](/2020/04/09/%E8%AE%A1%E7%BD%91/cn-3/tcp-establish.jpg)

第一、第二次握手的 seq 都是随机生成的，第一次握手无 ACK，其他正常。

第一、第二次握手的 SYN = 1，不能携带数据；第三次 SYN = 0，可以携带数据

若服务器的一个老第一次握手请求发送到了客户端，客户端会进行确认，但服务器会注意到过期的 ISN 编号，并忽略该第二次握手。

同样，客户端也会检查第二次握手中的 ISN 编号。

#### 四次挥手

![](TCP-close.png)

第一、第二次挥手可以携带数据，第三第四次不行（因为连接已断开）

### 拥塞控制

流量控制是收发双方间的，是为保证来得及接收而控制发送速度；
拥塞控制是防止网络中数据过多，使网络过载，而控制发送速度。

加性增加，乘性减少

![](/2020/04/09/%E8%AE%A1%E7%BD%91/cn-3/slow-start.jpg)

![](/2020/04/09/%E8%AE%A1%E7%BD%91/cn-3/tcp-congestion-control.jpg)

**TCP congestion-control algorithm**: (cwnd = congestion window, ssthresh = slow start threshold)

*   slow start：（指数，超时或初始进入，以窗口为1为开始）
    *   初始状态或出现超时时将发送窗口长度设置为1，此后每收到一个ACK则窗口长度+1（也就是每一轮之后翻倍）
    *   若窗口大小达到慢启动阈值则进入拥塞避免

> 窗口1+1=2后，发送的数据数也变为2，于是会收到2个ACK，则该RTT下窗口长度2+2=4，实现指数增长

*   congestion avoidance：（线性）
    *   收到新ACK时 cwnd = cwnd + MSS/cwnd

> MSS：最大报文段长度

*   fast recovery：（指数，三个重复ACK时进入，以窗口锐减为开始）
    *   每收到一个重复的ACK则恢复1个发送窗口长度（指数）
    *   收到了新的ACK则恢复拥塞避免
    *   若超时则进入慢启动状态，阈值设为窗口的一半，窗口设为1

- Tahoe：有重复三个 ACK 时将窗口设置为1（旧版）
- Reno：有重复三个 ACK 时将阈值设为先前窗口的一半，窗口为阈值（+3MSS）（常用）

![](tcp-reno&tahoe.jpg)

> 窗口减半后，即进入快速恢复后，若窗口指数增长，则还是快速恢复；若窗口线性增长，则是拥塞避免

TCP 平均吞吐率：3 / 4 W，W 为拥塞窗口大小

TCP 公平性：

![](/2020/04/09/%E8%AE%A1%E7%BD%91/cn-3/tcp-fairness.jpg)

从 A 开始，到 B 时丢包，减半至 C（C 为 B 与原点的中点），如此反复不断逼近最优点

# 4 网络层1：数据

## 虚电路和数据报网络

虚电路：预先建立好路线；数据报：每个报文单独走

### Virtual Circuit 虚电路

在废物 ATM 网络用过（不是自动柜员机啦

**一条虚电路在不同路段的编号不同**。如果相同，那要修改就会影响整个网络。

#### 转发表

|入接口|入VC号|出接口|出VC号|
|---|---|---|---|
|1|12|2|22|
|2|63|1|18|
|3|7|2|17|
|1|97|3|87|

每经过该路由器创建一个新虚电路，就会在表里加一项

~~虚电路是单向的~~（只是有些题目的设定罢了！）

#### 选路和转发

- 选路是在网络中寻找到目的节点的路径，通常依赖选路算法进行；
- 转发是在已知路径的基础上，根据路径选择下一个节点，以便转交数据包
- 两者的关联：选路是转发的基础。

### Datagram Network 数据报网络

#### 最长前缀匹配

Prefix Match|Link Interface
|---|---|
11001000 00010111 00010*** ********|0
11001000 00010111 00011000 ********|1
11001000 00010111 00011*** ********|2
otherwise |3

Ex：11001000 00010111 00011000 00011000 10101010 -> 1

一般而言，路由器仅需将部分地址转发至内网，其它的统统指向外网即可，于是不用记忆四十亿地址

## 路由器

### 输入排队

HOL（Head of the line）Blocking 是一个 由于其队伍前面的数据报被阻塞，导致即使其自己的目标出口畅通，也被阻塞

## IP（internet protocol）

- 无连接，不可靠
- 首部 20~24 字节

![](/2020/04/09/%E8%AE%A1%E7%BD%91/cn-4/ipv4.png)

- Time to live：每转发一次就减一，减到 0 时路由器必须抛弃该数据包
- Upper layer protocol：上层协议，仅会在到达终点的时候用到，6 = TCP，17 = UDP

### IPv4 数据包分片

分片可能在任一个节点进行，还可能出现多次分片

不同链路都有不同的最大传输单元 MTU（maximum transmission unit），即硬件限制。当要传输的数据包大于链路的 MTU 时，就要进行分片。

每次分片，IP 头部都会占用 20 字节。

- length：含 ip 头 的字节长度
- id：同一个分组的分片有相同 id
- flag：是否还有后续片
- offset：之前的（按原数据算）所有片的字节长度除以 8（不含 ip 头）

> 原数据总长也算了头部！

### IPv4 编址

IP 地址分给网卡而不是主机

![](/2020/04/09/%E8%AE%A1%E7%BD%91/cn-4/ipv4-addr.jpg)

