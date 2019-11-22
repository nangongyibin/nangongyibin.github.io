---
layout: post
title:   Visual Studio 2017安装时共享组件、工具和 SDK安装位置不能更改的问题  
category: C
tags: [C]
excerpt:  Visual Studio 2017安装时共享组件、工具和 SDK安装位置不能更改的问题
---

解决方案：

	删除注册表HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup下的SharedInstallationPath项。

参考网址：

<https://blog.csdn.net/caoxuqiang/article/details/82821692>


