# WHAT

当学习完hugo后，就觉得hugo是一个不错的框架，但是从完成md文档，到看到网页，整个流程相对wordpress这种还是显得太geek了。如果能有一个类似的写作流程和体验就完美了，于是就有了下面的内容。

这个repo是[http://www.goodmemory.cc](http://www.goodmemory.cc)的文章仓库，我们把githu当作博客写作工具，github的编辑器还是比Mon好用多了。在这里写的文章将会自动同步到目标网站，并转化成静态网页。

# HOW

1. 设置github的webservice hook。在收到push事件后，向目标网站发消息。
2. 目标网站收到消息后git pull，得到最新的文章内容
3. 调用本地的hugo，将markdown文章转化成html静态页面，并自动部署
流程图：
![](https://github.com/hiproz/hiproz.github.io/blob/master/goodmemory.cc/blog/images/2015/12/github-hugo-sync.jpg)
至此，只要在这里更新的内容，就自动转化成网站页面了。

# 文档头规范

---
title: 修改 wordpress 新建文章默认文件附件大小
author: admin
layout: post
date: 2013-06-15
url: /修改-wordpress-新建文章默认文件附件大小/
duoshuo_thread_id:
  - 6218977932405113601
categories:
  - 杂谈

---
have fun！
