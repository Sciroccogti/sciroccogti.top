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

## UDP

几乎等同裸的 IP，只能通过网络层（IP）提供的源地址信息分辨发送者

- 无连接传输，不可靠，可靠性要由应用层实现
- 首部 8 字节，总长不超过 64KB（$2^{16}$）
- 服务端一个套接字可接收多个客户端连接

![](/2020/04/09/计网/cn-3/udp.png)

### 校验

（每个字长 16 bit）

1. 每 16 位求和得到一个 32 位数
2. 若高 16 位不为 0，则高 16 位与低 16 位相加，得到新的 32 位数
3. 重复步骤 2 直到高 16 位为 0，将低 16 位 **取反** 得到校验和

> **取反**使得检验时只要将校验码和数据**一起相加**即可得到**全1**

能确保检测到 1bit 错误，2bit 及以上不一定能检测。

## TCP

- 可靠传输，有持续连接和非持续两种
- 首部 20~24 字节
- 服务端一个套接字仅服务一个客户端连接

### Reliable Data Transfer

参考：[可靠数据传输基本原理](https://blog.csdn.net/zy010101/article/details/88981728)

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
4. rdt 3.0：
   - 考虑数据丢失
   - 加入定时器 RTT，超时就重传

