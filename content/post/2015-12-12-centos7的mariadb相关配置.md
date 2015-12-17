---
title: centos7的mariadb相关配置
author: admin
layout: post
date: 2015-12-11
url: /centos7的mariadb相关配置/
categories:
  - 开发工具
  - 操作系统
  - 数据库

---
centos下面的repo源默认是支持mariadb的，因为是和mysql兼容的，所以如果特定需求，可以直接使用mariadb。

# 安装

yum -y install MariaDB-server MariaDB-client
  
or
  
yum -y install mysql

# 启动／停止／重启／重新加载配置

systemctl start|stop|restart|reload mariadb.service

# 修改密码

mysqladmin -u root password &#8216;root&#8217;

# 自动启动

systemctl enable mariadb.service

# 初次设置（密码／权限／库）

mysql\_secure\_installation