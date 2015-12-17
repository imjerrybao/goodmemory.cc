---
title: EC2 Instance 重启后ssh无法登陆的问题
author: admin
layout: post
date: 2014-01-16
url: /ec2-instance-重启后ssh无法登陆的问题/
categories:
  - 操作系统
tags:
  - ec2
  - ssh
format: aside

---
创建instance后，第一次都能正常运行，但是重启后大概率（大于80%）创建的instance就ssh连不上了。刚开始以为自己的业务导致服务器僵死，后来发现80端口都是正常的，说明服务器没有问题，只是ssh无法连接。
  
于是通过其他手段登录到服务器，想手动拉起sshd，系统提示：

<pre>Failed to start SSH server :
Starting sshd: /etc/ssh/sshd_config line 157: Bad yes/without-password/forced-commands-only/no argument: without-passwordUseDNS
[FAILED]</pre>

根据提示，发现sshd_config的配置中有非法的内容（没有换行），于是手动，修改后sshd正常启动。
  
进一步定位分析，发现原来 EC2的 instance 的/etc/rc.d/rc.local 中有脚本控制每次开机后向sshd_config 末尾写入：

<pre>UseDNS no
PermitRootLogin without-password</pre>

当这2行缺少合法的换行时，sshd就开机无法启动了。
  
解决方法：
  
1）屏蔽rc.local脚本的相关语句
  
2）修改sshd_config的属性为只读