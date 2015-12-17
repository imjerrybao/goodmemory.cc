---
title: Another MySQL daemon already running with the same unix socket
author: admin
layout: post
date: 2013-12-27
url: /another-mysql-daemon-already-running-with-the-same-unix-socket/
categories:
  - 数据库
tags:
  - mysql
format: aside

---
mysql mysql.sock被异常占用，导致进程无法拉起，删除mysql.sock，重启拉起进程  service mysqld restart