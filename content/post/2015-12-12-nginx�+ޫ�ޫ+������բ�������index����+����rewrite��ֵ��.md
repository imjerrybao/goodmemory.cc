---
title: nginx默认访问目录下的index文件的rewrite写法
author: admin
layout: post
date: 2015-12-12
url: /nginx默认访问目录下的index文件的rewrite写法/
categories:
  - nginx_resty

---
nginx 默认是支持index.html的, 比如你访问，默认等价于 xxx.com/abc/index.html。
  
但是访问 xxx.com/abc/ 时，怎么实现访问 xxx.com/abc/index.php？

做个简单的rewrite规则：

    location / {
    
    
        root   /var/www/phpshuo.com/;
        index  index.html index.htm;
    
        if (-f $request_filename/index.php){
                rewrite (.*) $1/index.php;
        }
        if (!-f $request_filename){
                rewrite (.*) /index.php;
        }
    
    
    }