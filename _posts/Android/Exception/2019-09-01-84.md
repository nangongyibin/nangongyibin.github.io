---
layout: post
title: AndroidStudio报错No cached version available for offline mode
category: Exception
tags: [Exception]
excerpt: AndroidStudio报错No cached version available for offline mode
---

打开的项目重新打开编译时

提示错误：

	Error:Could not resolve all files for configuration ‘:app:debugAnnotationProcessorClasspath’.

原因：

	 提高编译速度,在Gradle设置选项中开启了Offline work模式,解决办法关闭此选项

解决方式：
		
![](http://www.nangongyibin.com/assets/images/aeo1.png)


参考网址：

<https://blog.csdn.net/gerryrun/article/details/80335665>


