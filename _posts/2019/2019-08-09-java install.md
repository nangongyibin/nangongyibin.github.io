---
layout: post
title: java的安装
category: Linux
tags: [Linux]
excerpt: java的安装
---

### 1、安装文件下载 ###

    [https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html "下载地址")

### 2、将安装包上传到指定位置(我习惯放到：/usr/local/software/目录)，并解压 ###

    tar -zxvf jdk-8u144-linux-x64.tar.gz

### 3、配置JDK环境变量 ###

    vim /etc/profile
	在文本最后一行添加如下：
	#java environment
	export JAVA_HOME=/usr/java/jdk1.8.0_181
	export CLASSPATH=.:${JAVA_HOME}/jre/lib/rt.jar:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar
	export PATH=$PATH:${JAVA_HOME}/bin


### 4、让设置的环境变量生效 ###

    source /etc/profile

### 5、检查是否配置成功 ###

    java -version