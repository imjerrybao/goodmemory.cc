---
author: "admin"
date: 2015-12-18
title: 通过event-hook将github自动部署至Hugo网站
layout: page
url: /通过event-hook将github自动部署至Hugo网站/
aliases:
  - "/deploy-github-to-hugo-in-hook-event/"
  - "/deploy-github-to-hugo-in-hook-event.html"
  
---

## WHAT

hugo是一个轻量高效的博客系统，很适合个人博客。使用hugo，我们只要写作完markdown文档，就可以利用hugo工具，自动生成网页，
变成我们的网站。

我们理想的步骤：

* 在github上写完markdown文章
* 提交完后，数秒后就看见了我们的网站页面
* 在github上修改完网站的配置文件，数秒后我们的网站就变化和更新了。

好爽！

## 流程

为了完成上面的效果，我们大概分为几步：

 1. 设置github的webservice hook。当完成一篇新的文章或者修改旧的文章后，github就会向目标网站发webservice hook消息。
 2. 目标网站收到消息后git pull，解析消息特征，更新相关的文档，最后调用hugo
 3. hugo将markdown文章转化成html静态页面
 4. 将html页面部署到目标web服务器

![](http://hiproz.github.io/goodmemory.cc/blog/images/2015/12/github-hugo-sync.jpg)

## HOW
详细请移步：
<https://github.com/hiproz/hugo-sync>

分分钟就搞定了，一劳永逸！

have fun！
