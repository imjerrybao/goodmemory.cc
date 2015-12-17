---
title: myeclipse 2013 deploy path 修改
author: admin
layout: post
date: 2014-01-23
url: /myeclipse-2013-deploy-path-修改/
duoshuo_thread_id:
  - 6218977977665848065
categories:
  - 开发工具
tags:
  - deploy path
  - myeclipse
format: aside

---
文件路径：./.settings/org.eclipse.wst.common.component：

<project-modules id=&#8221;moduleCoreId&#8221; project-version=&#8221;1.5.0&#8243;>
  
<wb-module deploy-name=&#8221;web&#8221;>
  
<wb-resource deploy-path=&#8221;/&#8221; source-path=&#8221;/WebRoot&#8221; tag=&#8221;defaultRootSource&#8221;/>
  
<wb-resource deploy-path=&#8221;/WEB-INF/classes&#8221; source-path=&#8221;/src&#8221;/>
  
<property name=&#8221;context-root&#8221; value=&#8221;web&#8221;/>
  
<property name=&#8221;java-output-path&#8221; value=&#8221;/web/WebRoot/WEB-INF/classes&#8221;/>
  
</wb-module>
  
</project-modules>