---
title: EC2 security groups 生效问题
author: admin
layout: post
date: 2014-01-17
url: /ec2-security-groups-生效问题/
categories:
  - 开发工具
  - 操作系统
tags:
  - ec2
  - iptables
  - security groups
format: aside

---
EC2的security groups 机制和系统的iptables 服务是独立的，如果系统单独开了iptables 服务。security groups 效果是要求并集的。