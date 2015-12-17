---
title: EC2 snapshot 默认创建instance无法启动问题
author: admin
layout: post
date: 2014-01-16
url: /ec2-snapshot-默认创建instance无法启动问题/
categories:
  - 操作系统
tags:
  - aki
  - ec2
  - snapshot
format: aside

---
用创建的snapshot创建的 instance 一直显示&nbsp;initialization，查看log：
  
EXT3-fs: sda1: couldn&#8217;t mount because of unsupported optional features (240).
  
EXT2-fs: sda1: couldn&#8217;t mount because of unsupported optional features (240).
  
Kernel panic &#8211; not syncing: VFS: Unable to mount root fs on unknown-block(8,1)
  
初步分析，创建都是default 的，恢复也是default的，应该没有问题才对，但看日志，是文件系统不支持，说明内核版本有问题了。于是在恢复时手动选择AKI:
  
aki-68c06a69 [<img class="alignnone size-medium wp-image-713" alt="aki-config" src="http://www.goodmemory.cc/wp-content/uploads/2014/01/aki-config-800x214.png" width="800" height="214" />][1] 注意：此AKI要根据自己的系统以及版本选择合适的，我选择的只针对我自己的系统。
  
重新选择后，创建多个实例，都启动ok

 [1]: http://www.goodmemory.cc/?attachment_id=713#main