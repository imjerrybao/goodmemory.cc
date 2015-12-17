---
title: 如何使用ssh登录openshift
author: admin
layout: post
date: 2015-09-21
url: /如何使用ssh登录openshift/
categories:
  - 操作系统
tags:
  - openshift
  - ssh

---
openshift是免费的云平台，适合搞个公司网站或者个人blog。最近想把博客从openshift上迁移出去，wordpress本身有插件可以导出文章内容。但是对应的附件和图片利用导入工具，会有导入不完整的问题，简单的办法就是用ssh访问，将整个 uploads文件下载下来。

要支持ssh，openshift有一套安全机制。通过 rhc 上传key，实现无密码登录

具体参考：

<https://developers.openshift.com/en/getting-started-windows.html#client-tools>

如果不使用git，可以跳过 git的步骤。

ruby是从 [www.rubygems.org/gems/rhc][1]  下载的，需要自己搞定 vpn的问题。否则提示ssl失败

<p id="mqAZdab">
  <img class="alignnone size-full wp-image-947 " src="http://www.goodmemory.cc/wp-content/uploads/2015/09/img_55ff7c7a06f61.png" alt="" />
</p>

**安装rhc**
  
`openshift是免费的云平台，适合搞个公司网站或者个人blog。最近想把博客从openshift上迁移出去，wordpress本身有插件可以导出文章内容。但是对应的附件和图片利用导入工具，会有导入不完整的问题，简单的办法就是用ssh访问，将整个 uploads文件下载下来。

要支持ssh，openshift有一套安全机制。通过 rhc 上传key，实现无密码登录

具体参考：

<https://developers.openshift.com/en/getting-started-windows.html#client-tools>

如果不使用git，可以跳过 git的步骤。

ruby是从 [www.rubygems.org/gems/rhc][1]  下载的，需要自己搞定 vpn的问题。否则提示ssl失败

<p id="mqAZdab">
  <img class="alignnone size-full wp-image-947 " src="http://www.goodmemory.cc/wp-content/uploads/2015/09/img_55ff7c7a06f61.png" alt="" />
</p>

**安装rhc**
  
` 

可能出现的问题：\`no such file dl/import\`

<http://stackoverflow.com/questions/28896733/rhc-setup-gives-error-no-such-file-dl-import>

中间会提示输入openshift的账号和密码，成功后，会在本地.ssh 目录生成公私钥。并提示上传服务器。

**_这里要关注 .ssh的路径，后面客户端登录时要用到_**。

**ssh登录**

登录你的openshift账号，点击application ，进去就能看到详细的信息：

<p id="lLWhflu">
  <img class="alignnone size-full wp-image-948 " src="http://www.goodmemory.cc/wp-content/uploads/2015/09/img_55ff84fb5725d.png" alt="" />
</p>

根据右侧的账号和地址 ，用ssh就可以登录了

登录时选择key：

<p id="kLhwnWs">
  <img class="alignnone size-full wp-image-949 " src="http://www.goodmemory.cc/wp-content/uploads/2015/09/img_55ff858a43da8.png" alt="" />
</p>

这样就直接登录进去了，可以进行相关资料的备份了

&nbsp;

 [1]: http://rubygems.org/gems/rhc