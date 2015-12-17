---
title: postfix libmysqlclient 库缺失
author: admin
layout: post
date: 2013-09-16
url: /postfix-libmysqlclient-库缺失/
categories:
  - 操作系统
tags:
  - postfix

---
错误：postfix: error while loading shared libraries: libmysqlclient.so.16: cannot open shared object file: No such file or directory

解决：手动下载

cd /usr/lib64/

wget http://files.directadmin.com/services/debian\_5.0\_64/libmysqlclient.so.16