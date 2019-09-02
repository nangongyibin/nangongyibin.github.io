---
layout: post
title: java的安装
category: Linux
tags: [Linux]
excerpt: java的安装
---
### 1、检查是否存在open jdk，不存在直接跳到第 5 步 ###

	java -version
	
	查看当前系统自带的open jdk版本信息

### 2、查看包含java字符串的文件 ###


    rpm -qa | grep java
	ps:删除类似下面四个文件(不一定是四个)
	java-1.8.0-openjdk-1.8.0.102-4.b14.el7.x86_64
	java-1.8.0-openjdk-headless-1.8.0.102-4.b14.el7.x86_64

### 3、以.noarch结尾的文件不必删除 ###

    tzdata-java-2016g-2.el7.noarch
	javapackages-tools-3.4.1-11.el7.noarch


### 4、删除的具体命令 ###

	rpm -e --nodeps java-1.8.0-openjdk-1.8.0.102-4.b14.el7.x86_64
	rpm -e --nodeps java-1.8.0-openjdk-headless-1.8.0.102-4.b14.el7.x86_64


### 5、安装文件下载 ###

<https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html>

### 6、将安装包上传到指定位置(我习惯放到：/usr/local/software/目录)，并解压 ###

    tar -zxvf jdk-8u144-linux-x64.tar.gz

### 7、配置JDK环境变量 ###

    vim /etc/profile
	在文本最后一行添加如下：
	#java environment
	export JAVA_HOME=/usr/java/jdk1.8.0_181
	export CLASSPATH=.:${JAVA_HOME}/jre/lib/rt.jar:${JAVA_HOME}/lib/dt.jar:${JAVA_HOME}/lib/tools.jar
	export PATH=$PATH:${JAVA_HOME}/bin


### 8、让设置的环境变量生效 ###

    source /etc/profile

### 9、检查是否配置成功 ###

    java -version