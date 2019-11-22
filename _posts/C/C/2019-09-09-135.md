---
layout: post
title: Poco编译时一闪而过 
category: C
tags: [C]
excerpt: Poco编译时一闪而过 
---

### 编译POCO ###

Poco 根目录下有build_vs120.cmd和buildwin.cmd这两个批处理文件, 我们得修改一下它们。把build_vs120.cmd 修改为以下内容:


	@echo off
	    if defined VS100COMNTOOLS (
	       call "F:\Program Files (x86)\Microsoft Visual Studio 12.0\VC\bin\amd64\vsvars64.bat")
	     buildwin 120 build all both x64 sample

双击  build_vs100.cmd执行编译。完成后会在Poco根目录下的lib64中看到编译好的库。在bin64中有编译好的dll。

如果出现一闪而过的情况，需要到vs的D：\ SoftWare \ Microsoft Visual Studio 12.0 \ VC \ bin \ amd64 \目录下执行一下vcvars64.bat看是不是也是一闪而过或者提示“无法确定vs common tools文件夹的位置“。


解决方法：

	添加PATH环境变量，值为：C：\ Windows \ System32。再次双击就可以编译了。