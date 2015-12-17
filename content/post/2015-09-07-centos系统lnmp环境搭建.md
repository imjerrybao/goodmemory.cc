---
title: centos系统lnmp(nginx,mysql,php)环境搭建
author: admin
layout: post
date: 2015-09-07
url: /centos系统lnmp环境搭建/
categories:
  - php
tags:
  - centos
  - mysql
  - Nginx
  - php
  - vps
  - wordpress

---
新拿到vps，基本是裸机环境，如果要搞wordpress或者php后台，就需要php环境。

本来想手动安装，结果发现lnmp的一键脚本有更新。作者已经更新了1.2版本，基本都可以选择最新的版本了。<a href="http://lnmp.org/install.html" target="_blank">http://lnmp.org/install.html</a>

<p id="QhxjBBx">
  <img class="alignnone size-full wp-image-943 " src="http://www.goodmemory.cc/wp-content/uploads/2015/09/img_55ed733f88e98.png" alt="" />
</p>

安装成功!

如果你担心以上脚本的安全性，也可以自己亲手安装官方的版本

  * 安装mysql

<pre class="lang:default decode:true ">yum install -y mysql-server mysql mysql-deve</pre>

开机启动

<pre class="lang:default decode:true ">chkconfig mysqld on</pre>

设置密码

<pre class="lang:default decode:true">mysqladmin -uroot password 'newpassword'</pre>

  * 安装nginx

设置 yum源

<pre class="lang:default decode:true ">vi /etc/yum.repos.d/nginx.repo</pre>

<pre class="lang:default decode:true">[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/6/$basearch/
gpgcheck=0
enabled=</pre>

安装

<pre class="lang:default decode:true">yum install nginx</pre>

如果需要添加www 用户和组

<pre class="lang:default decode:true">groupadd -f www
useradd -g www www</pre>

  * 安装apache

安装apache 主要是因为wordpress的静态url路由需要相应的组件。

<pre class="lang:default decode:true ">yum install httpd</pre>

<pre class="lang:default decode:true ">chkconfig httpd on</pre>

&nbsp;

&nbsp;

&nbsp;

&nbsp;