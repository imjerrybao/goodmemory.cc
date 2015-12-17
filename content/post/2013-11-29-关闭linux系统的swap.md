---
title: 关闭Linux系统的swap
author: admin
layout: post
date: 2013-11-28
url: /关闭linux系统的swap/
duoshuo_thread_id:
  - 6218977965191987970
categories:
  - 操作系统
tags:
  - linux
  - swap
format: aside

---
临时关闭：执行 **swapoff -a** ，重启后又会开启swap。
  
永久关闭：注释掉 /etc/fstab 里的 swap 行，重启生效或者暂时swapoff -a，重启后不会再开启swap。