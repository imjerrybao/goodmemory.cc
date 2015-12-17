---
title: 关于IOS后台socket长连接的问题
author: admin
layout: post
date: 2015-08-18
url: /关于ios后台socket长连接的问题/
categories:
  - IOS
tags:
  - ios
  - 后台运行

---
1&#46; 进程退到后体后，只有3-10的时间，如果没有进一步处理，处于功耗考虑，socket就会被系统关闭。 2. ios8后，允许后台，ios8之前的版本，只能通过设置后台模式 Required background modes来实现，但如果本身没有voip功能，苹果审查会遭拒。 ①打开info.plist，添加下面的键值对： Required background modes ＝ App provides Voice over IP services ②配置XMPPStream的enableBackgroundingOnSocket属性为YES： _xmppStream.enableBackgroundingOnSocket = YES; 3. 参考 http://my.oschina.net/bankofchina/blog/281233 voip的方法，理论上定位消息也可以实现 4. 网上大段都是voip的例子，但按照苹果的审查规范，用voip实现后台keepalive 而没有实现voip是会被拒的。 综上所述，ios8以后，直接支持后台。ios8以前的，理论上gps位置信息也是可以在后台触发，从而通过策略实现长连接的，目前没有看到验证的例子，可以在这个方向下尝试下，毕竟所有的app都是需要位置服务器的，不属于伪造服务