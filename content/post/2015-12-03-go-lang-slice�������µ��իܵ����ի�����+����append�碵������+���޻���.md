---
title: Go lang Slice截取时指定最大容量以及append函数的使用说明
author: admin
layout: post
date: 2015-12-02
url: /go-lang-slice截取时指定最大容量以及append函数的使用说明/
categories:
  - Go
tags:
  - slice

---
slice是一个三元组对象
  
* 一个内容指针
  
* 有效内容长度
  
* 最大长度，也就是容量。

示例：

    package main
    
    import (
        "bytes"
        "fmt"
    )
    
    func main() {
        path := []byte("AAAA/BBBBBBBBB")
        sepIndex := bytes.IndexByte(path, '/')
        fmt.Println(sepIndex)
        dir1 := path[:sepIndex:sepIndex] //full slice expression
        fmt.Println(&path[0], &dir1[0])
        dir2 := path[sepIndex+1:]
        fmt.Println("dir1 =>", string(dir1)) //prints: dir1 => AAAA
        fmt.Println("dir2 =>", string(dir2)) //prints: dir2 => BBBBBBBBB
    
        dir1 = append(dir1, "suffix"...)
        fmt.Println(&dir1[0])
        path = bytes.Join([][]byte{dir1, dir2}, []byte{'/'})
    
        fmt.Println("dir1 =>", string(dir1)) //prints: dir1 => AAAAsuffix
        fmt.Println("dir2 =>", string(dir2)) //prints: dir2 => BBBBBBBBB (ok now)
    
        fmt.Println("new path =>", string(path))
    }
    

  * 第12行的代码就是一个指定容量的截取。
  * 如果增加后不回超出slice的最大空间，slice是不会重新分配对象的。但是如果空间不够，从13行和19行的地址打印输出我们可以看到，因为append超出了指定的空间容量，系统动态重新分配了空间，地址发生了变化。

运行结果：

4
  
0xc82000a3b0 0xc82000a3b0
  
dir1 => AAAA
  
dir2 => BBBBBBBBB
  
0xc82000a450
  
dir1 => AAAAsuffix
  
dir2 => BBBBBBBBB
  
new path => AAAAsuffix/BBBBBBBBB
  
成功: 进程退出代码 0.