---
title: 'MTK编译环境问题make: *** [mmi_feature_check] Error 1'
author: admin
layout: post
date: 2013-12-25
url: /mtk编译环境问题make-mmi_feature_check-error-1/
categories:
  - MTK
format: aside

---
今天遇到的问题:同样都是win7 系统,同样的安装路径,编译工具和代码,在新的机器上就是编译不了,提示如下:

make: \*** [mmi\_feature\_check] Error 1

熟悉mtk的同学一看就知道是路径问题.

于是在相关perl脚本中分段加打印,终于定位出原来是新的机器不支持命令行的空格缩写格式,不支持如  c:Progra~1 这样的写法.

具体原因待日后有时间再进一步定位.暂时通过修改工具路径规避此问题.