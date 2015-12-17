---
title: MAC gocede安装相关问题
author: admin
layout: post
date: 2015-10-28
url: /mac-gocede安装相关问题/
categories:
  - 开发工具

---
在安装go lang时，已经设置过GOPATH，go 也运行正常，但是安装 gocode时提示:
  
\`
  
Agreeing to the Xcode/iOS license requires admin privileges, please re-run as root via sudo.

package github.com/nsf/gocode: exit status 69
  
`当我们使用sudo 时，提示：`
  
package github.com/nsf/gocode: cannot download, $GOPATH not set. For more details see: go help gopath
  
`虽然之前已经设置，但是当切换权限时，也切换了环境变量，所以当用sudo管理员权限时提示没有设置环境变量。<br />
解决：`sudo env GOPATH=/Users/alex/dev/go go get -u github.com/nsf/gocode
  
\`
  
在命令行里临时指定env变量，完成