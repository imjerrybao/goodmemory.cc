---
title: mysql java 守护脚本
author: admin
layout: post
date: 2013-09-24
url: /mysql-java-守护脚本/
categories:
  - 操作系统
tags:
  - 守护脚本

---
参考网上资料，为生产环境的mysql 和java 进程增加守护进程，负责进程退出时，自动拉起

#!/bin/sh
  
##设置mysql进程和jira进程的监控进程名和进程数目；
  
mysql\_process\_check=\`lsof -i:3306|awk &#8216;{ print $1 }&#8217;|sed -n 2p\`
  
mysql_check=\`lsof -i:3306 |wc -l\`
  
jira\_process\_check=\`lsof -i:8080|awk &#8216;{ print $1 }&#8217;|sed -n 2p\`
  
jira_check=\`lsof -i:8080 |wc -l\`

##设置java运行环境，单独在shell脚本提示符号下面运行是可以不用设置java运行环境（因为加载用户shell脚本环境时已经加载
  
##了）；但是在cron进程下面时则需要设置java运行环境。

#export JAVA_HOME=/usr/lib/jvm/java-1.5.0-sun
  
#export PATH=$PATH:/usr/lib/jvm/java-1.5.0-sun/bin

while [ 1 ]
  
do
  
echo &#8220;$(date) jboss_deamon running&#8230;&#8221;
  
##先查看3306端口是否有运行进程（注意，这个时候运行在3306脚本上面的不一定是mysql进程mysqld！不过我们第一步是判断
  
##3306端口上面是否运行了进程）
  
while [ $mysql_check -eq 0 ]
  
do
  
echo &#8220;port:3306 have no process running&#8221;
  
sleep 2
  
#/usr/bin/mysqld_safe -umysql &
  
service mysql start
  
##如果8080端口上有进程运行，不管它是jira服务进程java还是其它进程，则一律把8080端口上运行的进程强行终止掉；
  
##因为jira服务的运行依赖于mysql的正常运行后才运行；如果jira服务进程正常存在系统中，但是mysql进程已经出问题了，
  
##那么这个时候不管8080端口上运行的是jira服务进程java还是其它进程，一律强行终止掉。
  
if [ $jira_check -gt 0 ]; then
  
pkill -9 $jira\_process\_check
  
fi
  
sleep 20
  
mysql_check=\`lsof -i:3306 |wc -l\`
  
done

##这一次将判断3306端口上面运行的是否为mysql进程mysqld，如果不是则强行终止3306上面的非mysql进程，同时终止完后运行##mysql进程
  
mysql\_process\_check=\`lsof -i:3306|awk &#8216;{ print $1 }&#8217;|sed -n 2p\`
  
if [ $mysql\_process\_check != mysqld ]; then
  
echo &#8216;mysql_process not run in port 3306,so I will kill process which run in port 3306.&#8217;
  
pkill -9 $mysql\_process\_check
  
mysql_check=\`lsof -i:3306 |wc -l\`
  
\# echo $mysql_check
  
while [ $mysql_check -eq 0 ]
  
do
  
sleep 2
  
#/usr/bin/mysqld_safe -umysql &
  
service mysql start
  
##确认8080端口上面是否运行了进程，如果运行了进程则强行终止掉8080端口上面运行的进程，不管是jira进程还是其它进程。
  
if [ $jira_check -gt 0 ]; then
  
pkill -9 $jira\_process\_check
  
fi
  
sleep 20
  
mysql_check=\`lsof -i:3306 |wc -l\`
  
done
  
echo &#8216;mysql_process are running in port 3306.&#8217;
  
else echo &#8216;mysql_process are running in port 3306.&#8217;
  
fi

##确认8080端口上面是否运行了进程（不管8080端口上面运行的是java进程还是其它进程）jira_check=\`lsof -i:8080 |wc -l\`
  
while [ $jira_check -eq 0 ]
  
do
  
echo &#8220;port:8080 have no process running&#8221;
  
sleep 2
  
#/usr/local/jira/bin/startup.sh
  
nohup /data/web/jboss-as-7.1.1.Final/bin/standalone.sh >/dev/null 2>&1 &
  
sleep 30
  
jira_check=\`lsof -i:8080 |wc -l\`
  
done

##检查8080端口上面是否运行着jira服务进程java，如果没有则先强行终止8080端口上面运行的进程；然后在启动jira服务
  
jira\_process\_check=\`lsof -i:8080|awk &#8216;{ print $1 }&#8217;|sed -n 2p\`
  
if [[ $jira\_process\_check != java ]]; then
  
echo &#8216;jira_process not run in port 8080,so I will kill process which run in port 8080.&#8217;
  
pkill -9 $jira\_process\_check
  
jira_check=\`lsof -i:8080 |wc -l\`
  
\# echo $jira_check
  
while [ $jira_check -eq 0 ]
  
do
  
sleep 2
  
#/usr/local/jira/bin/startup.sh
  
/data/web/jboss-as-7.1.1.Final/bin/standalone.sh >/dev/null 2>&1 &
  
sleep 30
  
jira_check=\`lsof -i:8080 |wc -l\`
  
done
  
echo &#8216;jira_process are running in port 8080.&#8217;
  
else echo &#8216;jira_process are running in port 8080.&#8217;
  
fi
  
sleep 60
  
done