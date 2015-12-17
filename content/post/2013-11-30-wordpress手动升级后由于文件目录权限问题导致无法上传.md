---
title: wordpress手动升级后由于文件目录权限问题导致无法上传附件
author: admin
layout: post
date: 2013-11-30
url: /wordpress手动升级后由于文件目录权限问题导致无法上传/
categories:
  - 开发工具
  - 操作系统
tags:
  - wordpress
  - 上传文件
  - 权限

---
手动升级wordpress 后，发现无法上传附件，于是仔细分析新文件夹和老备份文件的差异，发现是由于cp时改变了upload 文件夹属性导致。wordpress upload文件夹的 归属是 apache:apache  所以在手动更新文件时，要使用 -Rp 参数，保持原文件的属性不变。