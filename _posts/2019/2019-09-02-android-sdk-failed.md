---
layout: post
title: 解决AndroidSDK下载和更新失败“Connection to https://dl-ssl.google.com refused”的问题
category: Exception
tags: [Exception]
excerpt: 解决AndroidSDK下载和更新失败“Connection to https://dl-ssl.google.com refused”的问题
---

更新sdk，遇到了更新下载失败问题： 

	Fetching https://dl-ssl.google.com/android/repository/addons_list-2.xml
	Fetched Add-ons List successfully
	Fetching URL: https://dl-ssl.google.com/android/repository/repository-8.xml
	Done loading packages.
	Fetching https://dl-ssl.google.com/android/repository/addons_list-2.xml
	Failed to fetch URL https://dl-ssl.google.com/android/repository/addons_list-2.xml, reason: Connection to https://dl-ssl.google.com refused
	Fetched Add-ons List successfully
	Fetching URL: https://dl-ssl.google.com/android/repository/repository-8.xml
	Failed to fetch URL https://dl-ssl.google.com/android/repository/repository-8.xml, reason: HttpHostConnect Connection to https://dl-ssl.google.com refused
	Done loading packages.

解决方式：

	1.启动 Android SDK Manager ，打开主界面，依次选择「Tools」、「Options...」，弹出『Android SDK Manager - Settings』窗口；
	2.在『Android SDK Manager - Settings』窗口中，在「HTTP Proxy Server」和「HTTP Proxy Port」输入框内填入mirrors.neusoft.edu.cn和80，并且选中「Force https://... sources to be fetched using http://...」复选框。设置完成后单击「Close」按钮关闭『Android SDK Manager - Settings』窗口返回到主界面；
	3.依次选择「Packages」、「Reload」。

参考网址：

<https://www.cnblogs.com/yc-755909659/p/4073415.html>


