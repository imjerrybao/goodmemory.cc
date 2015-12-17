---
title: Too many connections
author: admin
layout: post
date: 2015-09-21
url: /too-many-connections/
categories:
  - 数据库
tags:
  - mysql

---
在php的日志里我们看到了如下的告警日志：
  
mysql_connect(): Too many connections

查看默认参数：
  
mysql> show variables;

实时修改：
  
mysql> set global wait_timeout=10;
  
Query OK, 0 rows affected (0.01 sec)

mysql> set GLOBAL max_connections=1024;
  
Query OK, 0 rows affected (0.00 sec)

注意 interactive\_timeout  和 wait\_timeout，根据不同场景，修改不同的参数。

还可以修改 my.cnf , 然后 重启 mysqld 服务。

还需要关注查询慢的本质原因：

1）DB是innodb 还是myisam

2)  高频查询的表的index创建是否合理

3）业务的mysql 语句写的是否合理

如果以上还搞不定，就需要考虑 分库分表 ， 加proxy 做集群来分流了。