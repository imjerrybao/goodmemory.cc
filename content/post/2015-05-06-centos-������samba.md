---
title: centos 配置samba
author: admin
layout: post
date: 2015-05-06
url: /centos-配置samba/
categories:
  - 操作系统
tags:
  - centos
  - samba

---
1. 配置静态ip

vi /etc/sysconfig/network-scripts/ifcfg-eth0

DEVICE=eth0
  
HWADDR=08:00:27:37:6B:FB
  
TYPE=Ethernet
  
UUID=56360903-aeda-4fde-a8c2-43ae10a18e42
  
ONBOOT=yes
  
NM_CONTROLLED=yes
  
BOOTPROTO=static
  
IPADDR=192.168.199.254
  
GATEWAY=192.168.199.1
  
NETMASK=255.255.255.0
  
DNS1=192.168.199.1

2. 安装 samba

yum install samba samba-client samba-swat

3. 创建linux 用户

[root@open ~]# adduser zcj
  
[root@open ~]# passwd zcj

创建samba 用户

smbpasswd -a zcj

4. 配置samba

/etc/samba/smb.conf

几个关键配置：

1. Network Related Options

interfaces = lo eth0 192.168.xxx.xxx
  
hosts allow = 192.168.xxx.

这个配置很关键否则就会出现：NT\_STATUS\_INVALID\_NETWORK\_RESPONSE

2.  Share Definitions

这个配置根据目录和用户的权限不同而不同.

1) 简单无限制共享

[dev]
  
comment =  workspace
  
path = /home/dev/
  
public = yes

2）单用户授权：

[dev1]
  
comment = dev1 workspace
  
path = /home/dev1/
  
public = no
  
admin users = dev1
  
valid users = dev1
  
writable = yes
  
create mask = 0777
  
directory mask = 0777

3）其他配置：

可参考：<a href="http://www.cnblogs.com/mchina/archive/2012/12/18/2816717.html" target="_blank">http://www.cnblogs.com/mchina/archive/2012/12/18/2816717.html</a>

4) 防火墙

其他问题：

1. session setup failed: NT\_STATUS\_LOGON_FAILURE：

通过 smbpasswd 添加samba 用户

2. tree connect failed: NT\_STATUS\_BAD\_NETWORK\_NAME

关闭selinux：**/etc/selinux/config. Change the line SELINUX=enforcing to SELINUX=permissive or SELINUX=disabled**