---
title: Windows netstat 查看端口、进程占用
author: admin
layout: post
date: 2013-08-21
url: /windows-netstat-查看端口、进程占用/
categories:
  - 操作系统
tags:
  - windows下的netstat

---
很多用惯linux的同学，遇到windos的端口占用时就很不习惯，因为命令参数调用习惯等都不同，下面的文章很不错，值得收藏。

原网址：<http://ywsm.iteye.com/blog/510670>

&nbsp;

目标：在Windows环境下，用netstat命令查看某个端口号是否占用，为哪个进程所占用.

操作：操作分为两步：（1）查看该端口被那个PID所占用;方法一：有针对性的查看端口，使用命令

Netstat –ano|findstr “<端口号>”,如图，最后一列为PID。图中的端口号为1068，所对应的PID为3840。

&nbsp;

(a)图

方法二：查看所有的，然后找到对应的端口和PID。

&nbsp;

(b)图

第一幅图中的5列就是上面(a)图对应的5列

（2）查看该PID对应的进程名称。

方法一：一直用命令查找，tasklist|findstr “<PID号>”

&nbsp;

(c)图

从 (c)图 可以看出，PID为3840所对应的进程名字为msnmsgr.exe。

方法二：用任务管理器查看。

调出任务管理器，选择列，如d图。

(d)图

查看PID对应的进程名称。如(e)图中的msnmsgr.exe

&nbsp;

&nbsp;

(e)图

附录：在命令行中输入netstat /? 可以查看netstat的相关信息。

C:Documents and SettingsAdministrator>netstat /?

显示协议统计信息和当前 TCP/IP 网络连接。

NETSTAT \[-a\] \[-b\] \[-e\] \[-n\] \[-o\] \[-p proto\] \[-r\] \[-s\] \[-t\] \[-v\] [interval]

-a            显示所有连接和监听端口。

-b            显示包含于创建每个连接或监听端口的

可执行组件。在某些情况下已知可执行组件

拥有多个独立组件，并且在这些情况下

包含于创建连接或监听端口的组件序列

被显示。这种情况下，可执行组件名

在底部的 [] 中，顶部是其调用的组件，

等等，直到 TCP/IP 部分。注意此选项

可能需要很长时间，如果没有足够权限

可能失败。

-e            显示以太网统计信息。此选项可以与 -s

选项组合使用。

-n            以数字形式显示地址和端口号。

-o            显示与每个连接相关的所属进程 ID。

-p proto      显示 proto 指定的协议的连接；proto 可以是

下列协议之一: TCP、UDP、TCPv6 或 UDPv6。

如果与 -s 选项一起使用以显示按协议统计信息，proto 可以是下列协议之一:

IP、IPv6、ICMP、ICMPv6、TCP、TCPv6、UDP 或 UDPv6。

-r            显示路由表。

-s            显示按协议统计信息。默认地，显示 IP、

IPv6、ICMP、ICMPv6、TCP、TCPv6、UDP 和 UDPv6 的统计信息；

-p 选项用于指定默认情况的子集。

-t            显示当前连接卸载状态。

-v            与 -b 选项一起使用时将显示包含于

为所有可执行组件创建连接或监听端口的

组件。

interval      重新显示选定统计信息，每次显示之间

暂停时间间隔(以秒计)。按 CTRL+C 停止重新

显示统计信息。如果省略，netstat 显示当前

配置信息(只显示一次)