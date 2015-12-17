---
title: 使用Sublime Text3+Ctags+Cscope替代Source Insight
author: admin
layout: post
date: 2015-05-05
url: /使用sublime-text3ctagscscope替代source-insight/
categories:
  - 操作系统

---
参考：https://www.zybuluo.com/lanxinyuchs/note/33551

**说明**：以Windows系统下查看C++代码为例。因为Source Insight(以下简称SI)是收费软件，且界面丑陋，所以考虑其替代方案，发现Sublime Text3(以下简称ST3) + Ctags + Cscope 可以取得很好的效果。使用ST3基本可以实现全键盘操作，同时它又没有学习Vim的陡峭曲线。

<div class="md-section-divider">
</div>

### **安装方法**： {#安装方法}

<div class="md-section-divider">
</div>

#### 1. 安装Package Control for ST3 {#1-安装package-control-for-st3}

<div class="md-section-divider">
  <span style="color: #ff0000;"> https://packagecontrol.io/installation</span>
</div>

#### 2. 安装Ctags插件 {#2-安装ctags插件}

(1) 通过 Preference -> Package Control -> Install Package安装Ctags插件
  
(2) 下载 Ctags.exe, 通过 Preference -> Package Settings -> Ctags -> Settings Default 中的内容拷贝到 Setting User中，将 `command": ""` 中的 `""` 填入Ctags.exe的路径位置
  
(3) 在工程根目录上点击右键，选择`Ctags:Rebuild tags`

<div class="md-section-divider">
</div>

#### 3. 安装Cscope插件 {#3-安装cscope插件}

(1) 通过 Preference -> Package Control -> Install Package安装Cscope插件
  
(2) 下载 Cscope.exe, 并在工程根目录下生成cscope.out文件
  
(3) 打开CscopeSublime.sublime-settings文件(可能需要添加到 Package -> User 目录下)，将 `"executable": ""` 中的`""` 填入Cscope.exe的路径位置,将 `"database_location": ""` 中的 `""`填入cscope.out的路径位置

<div class="md-section-divider">
</div>

### **功能实现：** {#功能实现}

(1) 对于symbol函数的定义查询，ST3自带此功能`Go to Definition`，且搜索结果有多个时可以预览，不用跳转到另一个文件。Ctags也有此功能`navigate_to_definition`，搜索结果比ST3要准确一些，但多结果时不支持预览。Csope也有此功能 `Cscope: look up function defintion`，但搜索结果不支持双击点开。因此实际中多用ST3和Ctags来实现此功能
  
(2) 对于symbol变量的定义查询，ST3不支持，Ctags有此功能，方法同其查询symbol函数的定义一致。Cscope也可以用查询symbol函数定义的方法实现此功能，搜索结果不支持双击点开。因此实际中多用Ctags来实现此功能
  
(3) 对于函数caller的查询，只有Cscope有此功能`Cscope: look up function calling this function`
  
(4) 全局搜索, ST3可通过`Ctrl+Shift+F`实现，但搜索耗时较长。Cscope可通过`Cscope: look up symbol`实现，因为已经通过cscope.out建立了索引，所以结果很快，但结果不一定全面

**注**：使用Cscope的功能时，需按`enter`键确定才会执行

**比较**：ST3 + Ctags + Cscope的方案基本可以实现Source Insight的常用有效功能（除了查看类继承关系的Relation Windows），且其速度更快，界面也更为清爽。ST3相比于SI的其他优点还包括：
  
(1)ST3使用`Ctrl+P`搜索文件时，使用的是模糊匹配，不像SI必须顺次拼写正确才行
  
(2)ST3支持tab模式，可方便的在多个文件间切换

<div class="md-section-divider">
</div>

### **ST3实用技巧**： {#st3实用技巧}

(1) `Alt+O`可以实现头文件和源文件之间的快速切换
  
(2) 通过 View -> Side bar 可在左侧显示当前打开的文件列表
  
(3) ST3虽然不像notepad++可以在sidebar上显示函数列表，但是可通过`Ctrl+R`查看
  
(3) 通过 Preference -> Key binding user 可根据个人操作习惯自定义快捷键（包括ST3自带的和插件的）
  
(4) 双击可选中光标所在单词，三击可选中光标所在行
  
(5) `Ctrl+Shift+T`可以打开之前关闭的tab页，这点同chrome是一样的