---
title: linux sync 木马 .Iptables .Iptablex
author: admin
layout: post
date: 2014-01-19
url: /linux-sync-木马-iptables-iptablex/
categories:
  - 操作系统
tags:
  - .Iptablex
  - iptables
  - sync
format: aside

---
现象：linux 主机对外发出高达上G的流量定向攻击互联上的某台主机（1001端口），结果就是，目标挂掉了，你也被云主机封号了（这种攻击会导致云架构共享的网络瘫痪，所有用户无法正常服务，属于致命问题）。

对于站长来说封号就是灭顶之灾，如果数据无法备份，就更悲剧了。

目前木马攻击的注入方式未知，希望有高人研究，根据本人主机的情况，猜测ssh扫描，bug注入的可能性比较高。

防范：

1. 修改ssh默认端口

2. 修改ssh的访问源ip（类似 AWS EC2 的security groups 功能）

同样问题的站长：

<http://bbs.chinaunix.net/thread-4118890-1-1.html>

<http://www.xujiansheng.cn/2014/01/linux-viruses-iptablex-iptables/>

可疑样本文件：<a href="http://www.goodmemory.cc/?attachment_id=" rel="attachment wp-att-732">Iptablex.zip</a>

希望有高人能看到，能发现后门，造福广大站长

经这两天学习和热心网友乌云微博管理员的帮助，初步定位是struct 漏洞：

类似：<http://www.beardnote.com/?p=829>

&nbsp;

<pre>解决struts2最新s2-016代码执行漏洞–CVE-2013-2251

今天接到外界报告struts2框架存在任意命令执行漏洞，可直接执行任意系统命令。 详细见官方说明：http://struts.apache.org/release/2.3.x/docs/s2-016.html

漏洞版本:
Apache Struts 2.0.0 – Apache Struts 2.3.15

漏洞描述:
CVE-2013-225. Struts2 是第二代基于Model-View-Controller (MVC)模型的java企业级web应用框架。它是WebWork和Struts社区合并后的产物

Apache Struts2的action:、redirect:和redirectAction:前缀参数在实现其功能的过程中使用了Ognl表达式，并将用户通过URL提交的内容拼接入Ognl表达式中，从而造成攻击者可以通过构造恶意URL来执行任意Java代码，进而可执行任意命令

redirect:和redirectAction:此两项前缀为Struts默认开启功能，目前Struts 2.3.15.1以下版本均存在此漏洞

目前Apache Struts2已经在2.3.15.1中修补了这一漏洞。强烈建议Apache Struts2用户检查您是否受此问题影响，并尽快升级到最新版本

&lt; 参考 1. http://struts.apache.org/release/2.3.x/docs/s2-016.html &gt;

测试方法:
@Sebug.net dis 本站提供程序(方法)可能带有攻击性,仅供安全研究与教学之用,风险自负!

由于Apache Struts2 在最新修补版本2.3.15.1中已经禁用了重定向参数，因此只要重定向功能仍然有效，则说明受此漏洞影响：

http://host/struts2-showcase/employee/save.action?redirect:http://www.yahoo.com/

如果页面重定向到www.yahoo.com，则表明当前系统受此漏洞影响。

验证表达式解析和命令执行：

http://host/struts2-showcase/employee/save.action?redirect:%25{3*4}

http://host/struts2-showcase/employee/save.action?redirect:%25{(new+java.lang.ProcessBuilder(new+java.lang.String[]{'command','goes','here'})).start()}`
Sebug安全建议:

厂商状态：
厂商已经发布Apache Struts 2.3.15.1以修复此安全漏洞，建议Struts用户及时升级到最新版本。

厂商安全公告：S2-01. 链接：http://struts.apache.org/release/2.3.x/docs/s2-016.html

软件升级页面：http://struts.apache.org/download.cgi#struts23151

目前存在漏洞的公司
乌云上，已经发布了快60个struts的这个漏洞问题，包括腾讯，百度，网易，京东等国内各大互联网公司。（http://www.wooyun.org/bugs/new_submit/） 
<img alt="" src="http://bcs.duapp.com/beardnote/2013/07/23931374053684.png" />
解决办法：
升级到Struts 2.3.15.1（强烈建议）
使用ServletFilter来过滤有问题的参数（临时替换方案）
<img alt="" src="http://bcs.duapp.com/beardnote/2013/07/2881374053684.jpg" /> 
参考资料:
http://sebug.net/appdir/Apache%20Struts

这次struts爆出来的漏洞,一大片的网站受的影响,影响最严重的就是电商了. 对于struts的漏洞,曾经也写过struts2代码执行漏洞,struts2自从使用OGNL表达式的方式后,经常就会报出一些可怕的漏洞出来,建议那些还是struts的童鞋们,学习一些其他的框架吧!比如,spring mvc,简单,好用,高效! 这里有篇对struts漏洞分析很透彻的文章,推荐学习学习. http://www.inbreak.net/archives/507</pre>

问题解决参考：
  
<http://www.geek521.com/?p=3278>