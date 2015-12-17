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
1.修改 /etc/php.ini

修改如下参数：

upload\_max\_filesize=2M

post\_max\_size=8M

2. 重启服务

service httpd restart