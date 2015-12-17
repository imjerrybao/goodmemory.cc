---
title: Primary script unknown
author: admin
layout: post
date: 2015-12-11
url: /primary-script-unknown/
categories:
  - nginx_resty

---
# nginx运行时的error log：

FastCGI sent in stderr: &#8220;Primary script unknown&#8221; while reading response header from upstream 原因在于nginx 默认的脚本配置中

    location ~ \.php$ { 
        root html; fastcgi_pass 127.0.0.1:9000; 
        fastcgi_index index.php; 
        fastcgi_param SCRIPT_FILENAME /script$fastcgi_script_name; 
        include fastcgi_params; 
    } 
    

# SCRIPT_FILENAME 需要更新成实际的目录，修改如下：

    $document_root$fastcgi_script_name;