---
title: RVCT 远程license 问题
author: admin
layout: post
date: 2014-08-23
url: /rvct-远程license-问题/
categories:
  - MTK
tags:
  - mtk

---
错误:

Error: C9932E: Cannot obtain license for Compiler (feature compiler) with licens
  
e version >= 3.1:
  
Terminal Server remote client not allowed.
  
Feature: compiler
  
License path: D:ARMLicenseslicense.lic
  
FLEXnet Licensing error:-103,577
  
For further information, refer to the FLEXnet Licensing End User Guide,
  
available at &#8220;www.macrovision.com&#8221;.

解决：<span style="color: #000000;">rvds.dat里HOSTID=XXXXX之后加上TS_OK就可以了</span>