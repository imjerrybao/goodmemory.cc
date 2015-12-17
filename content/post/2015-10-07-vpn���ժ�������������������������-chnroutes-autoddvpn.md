---
title: vpn时如何自动区分国内国外-chnroutes-autoddvpn
author: admin
layout: post
date: 2015-10-07
url: /vpn时如何自动区分国内国外-chnroutes-autoddvpn/
categories:
  - 操作系统
tags:
  - autoddvpn
  - chnroutes
  - github

---
针对这个需求，有专门的开源项目&nbsp;<span>chnroutes</span> 

最起源的代码仓库：<a href="https://code.google.com/p/chnroutes/" target="_blank">https://code.google.com/p/chnroutes/</a> 

<span style="line-height:1.5;">1.&nbsp;</span>与这个最接近的github上的代码: 

<a href="https://github.com/fivesheep/chnroutes" target="_blank">https://github.com/fivesheep/chnroutes</a> 

<span style="line-height:1.5;">2.</span><span style="line-height:1.5;">&nbsp;</span>还有一个差异比较大的，从时间上看是比较旧的，但需要比较代码才能知道哪个更合适 

<a href="https://github.com/jimmyxu/chnroutes" target="_blank">https://github.com/jimmyxu/chnroutes</a> 

<span style="line-height:1.5;">3.&nbsp;</span>还有一个改进版，提供 go python 以及window界面版本，<span style="line-height:1.5;">从其文档连接看是以&nbsp;</span><a href="https://github.com/fivesheep/chnroutes" target="_blank">fivesheep</a><span style="line-height:1.5;">&nbsp;的版本为基线版本。</span> 

<a href="https://github.com/sabersalv/freedom-routes" target="_blank">https://github.com/sabersalv/freedom-routes</a>&nbsp; 



本文验证了pptp windows 环境下的功能，工作OK。 

其中python 使用 2.7.10 版，请安装完整版，因为可能需要其他关联库。 

脚本执行要使用管理员权限。 

1，2，3生成的路由数据略有差异，经简单测试，以 baidu.com 和weibo.com 为test case， 似乎3的效果好些，但因每人宽带出口不同，不作为唯一结论，使用者请自行测试。 



如果要让路由器实现上述功能，提供用户透明的vpn体验，也有相应的项目&nbsp;&nbsp;<a href="https://code.google.com/p/autoddvpn/" target="_blank">https://code.google.com/p/autoddvpn/</a>