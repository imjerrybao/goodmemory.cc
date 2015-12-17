---
title: ‘xxx’is marked as crashed and should be repaired
author: admin
layout: post
date: 2013-12-01
url: /xxxis-marked-as-crashed-and-should-be-repaired/
categories:
  - 数据库
tags:
  - crashed
  - mysql
  - repir table
format: aside

---
1、从网上查了下有的说是频繁查询和更表造成的索引错误。

2.还有说法为是MYSQL数据库因为某种原因而受到了损坏，如：数据库服务器突发性的断电、在提在数据库表提供服务时对表的原文件进行某种操作都 有可能导致MYSQL数据库表被损坏而无法读取数据。总之就是因为某些不可测的问题造成表的损坏。

修复：

mysql> REPAIR TABLE int\_dev\_gps;