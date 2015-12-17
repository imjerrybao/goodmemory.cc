---
title: 服务器shell脚本中用wget/curl模拟客户端调用api接口
author: admin
layout: post
date: 2013-11-30
url: /服务器shell脚本中用wgetcurl模拟客户端调用api接口/
categories:
  - 操作系统
tags:
  - curl
  - shell
  - 模拟客户端
format: aside

---
目前的生产环境使用的vps的shell监护脚本中，发现有很大的概率reboot命令会僵死，但是web页面面板功能正常。正好网站提供了api接口，所以可以通过api完成可靠的系统复位。

我们可以在shell中用wget 和curl 模拟客户端，来发送指令的url.

curl 常用的 开关：

-o 忽略下载

-s 忽略返回

其他的见 &#8211;help

样例：

curl -o /dev/null -s &#8220;http://xxxx.com&#8221;