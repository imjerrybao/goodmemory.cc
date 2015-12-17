---
title: centos VPS 下安装使用iostat
author: admin
layout: post
date: 2013-11-30
url: /centos-vps-下安装使用iostat/
categories:
  - 操作系统
tags:
  - iostat
format: aside

---
新增的centos vps 发现没有iostat，而且 yum install iostat 失败。

1. 安装

\# yum install sysstat

2. 启动

\# /etc/init.d/sysstat start

3. 使用

\# iostat -x 1

每1秒刷新1次