---
title: jboss 的时区问题导致timestamp 错误
author: admin
layout: post
date: 2013-09-15
url: /jboss-的时区问题导致timestamp-错误/
categories:
  - 开发工具
tags:
  - jboss 时区

---
最近由于更换云主机，环境进行了搬迁，发现以前正常的设备数据都和实际时间段差了时区值。同时发现jboss的日志时间是UTC时间，所以推断是jboss时间错误导致时间戳错误，数据错乱。

修改jboss 时区：

修改 xxx/bin/xxx.cnf xxx根据服务器类型有变化

在 启动配置中添加jvm 参数，指定时区和jboss 的语言：

export JAVA_OPTS=&#8221;-Duser.timezone=Asia/Shanghai -Dfile.encoding=utf-8 -Duser.language=zh -Duser.region=CN&#8221;