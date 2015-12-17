---
title: mysql table crash 自动修复脚本
author: admin
layout: post
date: 2013-12-02
url: /mysql-table-crash-自动修复脚本/
categories:
  - 数据库
tags:
  - crash table
  - 修复脚本
format: aside

---
已验证：eg1：

#!/bin/sh

cd /var/lib/mysql

echo &#8220;$(date) start mysql_deamon running&#8230;&#8221;
  
sleep 180

while [ 1 ]
  
do
  
echo &#8220;$(date) mysql_deamon running&#8230;&#8221;
  
sleep 30

for i in \`cat mysqld.log |grep crash|awk -F &#8220;&#8216;&#8221; &#8216;{print $2}&#8217;|sort -u|sed -e &#8216;1d&#8217; \`;
  
do
  
<span style="color: #ff0000;">if [ &#8220;$i&#8221; != &#8220;./xxx/xxx&#8221; ]; then</span>
  
 <span style="color: #ff0000;">echo &#8216;not find xxx crash&#8217;</span>
  
 <span style="color: #ff0000;">else</span>
  
 <span style="color: #ff0000;">echo &#8216;find xxx crash&#8217;</span>
  
 <span style="color: #ff0000;">echo &#8216;repair xxx&#8217;</span>
  
 <span style="color: #ff0000;">mysqlcheck -uxxx -pxxx xxx xxx -r</span>
  
 <span style="color: #ff0000;">fi</span>

echo &#8216;clear the err log&#8217;
  
> mysqld.log
  
done
  
done

eg1 中红色部分代码其实可以1句搞定，由于本人不善 shell 提取字符操作，只能做固定判断了

未验证 eg2:

<pre><span style="font-family: Georgia, 'Times New Roman', 'Bitstream Charter', Times, serif; font-size: 13px; line-height: 19px;">#!/bin/bash</span></pre>

#This script edit by badboy connect leezhenhua17@163.com
  
#This script used by repair tables
  
mysql_host=localhost
  
mysql_user=root
  
mysql_pass=123456   #密码如果带特殊字符如分号可以这么写  root;2010就可以了
  
database=test

tables=$(mysql -h$mysql\_host -u$mysql\_user -p$mysql_pass $database -A -Bse “show tables”)
  
for arg in $tables
  
do
  
check\_status=$(mysql -h$mysql\_host -u$mysql\_user -p$mysql\_pass $database -A -Bse “check table $arg” | awk ‘{ print $4 }’)
  
if [ &#8220;$check_status&#8221; = &#8220;OK&#8221; ]
  
then
  
echo “$arg is ok”
  
else
  
echo $(mysql -h$mysql\_host -u$mysql\_user -p$mysql_pass $database -A -Bse “repair table $arg”)

fi
  
echo $(mysql -h$mysql\_host -u$mysql\_user -p$mysql_pass $database -A -Bse “optimize table $arg”)
  
done

未验证 eg3:

#!/bin/bash
  
#author:itnihao
  
#mail:itnihao@qq.com
  
#date 2013-02-18
  
#version v1.0
  
#function:repair mysql table

User=root
  
Password=123456
  
Host=192.168.1.10
  
Database=$(mysql -u${User} -p${Password} -h${Host} -e &#8216;show databases&#8217;|grep -v &#8216;Database&#8217;)
  
for DBname in ${Database}
  
do
  
table=$(mysql -u${User} -p${Password} -h${Host} ${DBname} -e &#8216;show tables&#8217;|grep -v tables\_in\_mysql)
  
for tableName in ${table}
  
do
  
mysql -u${User} -p${Password} -h${Host} ${DBname} -e &#8220;check table ${tableName}&#8221; [ &#8220;$?&#8221; != 0 ] &&mysql -u${User} -p${Password} -h${Host} ${DBname} -e &#8220;repair table ${tableName}&#8221;
  
done
  
done