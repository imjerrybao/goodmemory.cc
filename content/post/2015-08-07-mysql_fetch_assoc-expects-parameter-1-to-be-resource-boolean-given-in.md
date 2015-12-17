---
title: mysql_fetch_assoc() expects parameter 1 to be resource, boolean given in
author: admin
layout: post
date: 2015-08-07
url: /mysql_fetch_assoc-expects-parameter-1-to-be-resource-boolean-given-in/
categories:
  - 数据库

---
参考：http://stackoverflow.com/questions/20423037/warning-mysql-fetch-assoc-expects-parameter-1-to-be-resource-boolean-given-i

本质就是没有对入参做异常判断。