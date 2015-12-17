---
title: You have not agreed to the Xcode license agreements
author: admin
layout: post
date: 2015-10-28
url: /you-have-not-agreed-to-the-xcode-license-agreements/
categories:
  - IOS

---
在安装gocode时，提示You have not agreed to the Xcode license agreements 相关的错误提示：
  
`You have not agreed to the Xcode license agreements, please run 'xcodebuild -license' (for user-level acceptance) or 'sudo xcodebuild -license' (for system-wide acceptance) from within a Terminal window to review and agree to the Xcode license agreements.`
  
根据提示，执行 sudo xcodebuild -license 或者直接通过系统运行 xcode，会出现 license界面，点击同意，再次安装就ok了