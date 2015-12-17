---
title: xcode pod 路径下头文件的“file not found”问题
author: admin
layout: post
date: 2015-10-15
url: /xcode-pod-路径下头文件的file-not-found问题/
categories:
  - IOS
tags:
  - pod

---
更换了电脑，重新从git上下拉的工程，发现头文件命名存在，但是编译时提示 “file not found”的问题，初步怀疑环境配置问题，因为之前的环境是ok的。但检查比对了pod和主工程的路径，没发现明显的线索。 

所以就重新创建了pod的工作区： 

把.xcworkspace,pod开头的文件除了Podfile,全删，然后重新pod install/update，再打开新的xcworkspace 文件，编译，ok