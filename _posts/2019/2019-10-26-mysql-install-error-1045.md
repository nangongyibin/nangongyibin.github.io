---
layout: post
title:   安装MySQL最后一步出现错误Error Nr.1045解决方法  
category: MySql
tags: [MySql]
excerpt:  安装MySQL最后一步出现错误Error Nr.1045解决方法
---


安装MySQL最后一步出现错误Error Nr.1045

![](http://www.nangongyibin.com/assets/images/mer1.png)

解决方案：

	1.停止MySQL服务：这台电脑-->右键 管理-->服务和应用程序-->服务 找到名为"MySQL"的服务 右键停用
	
	2.进控制面板卸载MySQL
	
	3.进入系统通用的数据文件夹删除MySQL文件夹

	win7/8/8.1/10目录：C:\ProgramData或者%ProgramData%

	4.重新安装 这次不报错了

参考网址：

<https://blog.csdn.net/gsls200808/article/details/46846019>

