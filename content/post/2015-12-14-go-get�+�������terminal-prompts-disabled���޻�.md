---
title: go get引起的terminal prompts disabled错误
author: admin
layout: post
date: 2015-12-14
url: /go-get引起的terminal-prompts-disabled错误/
categories:
  - Go

---
执行go get命令时，出现如下的错误提示

    fatal: could not read Username for 'https://github.com': terminal prompts disabled
    

两种解决方案：

  1. 先通过ssh成功登陆一次git，正确获取到key缓存。
  2. 手动添加key：
  
    [Generating SSH keys][1]

然后就可以正常get了。

文章参考：
  
[terminal prompts disabled][2]

 [1]: https://help.github.com/articles/generating-ssh-keys/
 [2]: http://stackoverflow.com/questions/32232655/go-get-results-in-terminal-prompts-disabled-error-for-github-private-repo