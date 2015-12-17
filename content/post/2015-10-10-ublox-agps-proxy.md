---
title: ublox agps proxy
author: admin
layout: post
date: 2015-10-10
url: /ublox-agps-proxy/
categories:
  - Git
  - 硬件
tags:
  - agps proxy

---
1. 修复了一个bug：每当有请求时，都会产生一个子进程，响应后子进程不退出，导致内存泄漏 

2. 遗留的bug：按照原来的设计，socket建链后，只有client 发送 身份请求，验证成功后，才响应，目前是在 accept 建链时，就主动回应数据 

代码地址：&nbsp;https://github.com/hiproz/ubx\_agps\_proxy<a href="https://github.com/hiproz/ubx_agps_proxy" target="_blank">https://github.com/hiproz/ubx_agps_proxy</a>