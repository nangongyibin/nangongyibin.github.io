---
layout: post
title: Mongodb的安装
category: Linux
tags: [Linux]
excerpt: Mongodb的安装
---

## 1、创建文件 ##


	cd /usr/local/
	mkdir mongodb
	cd ./mongodb/
	mkdir data;mkdir log
	cd ./data/
	mkdir db
	cd /usr/local/


## 2、下载Mongodb ##

	wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-4.0.1.tgz（这里使用4.0历史版本，亚马逊版本不能安装，出错glibc libc.so.6: version GLIBC_2.18 not found）

## 3、解压 ##

	tar -zxvf mongodb-linux-x86_64-4.0.1.tgz(解压后可以删除rm mongodb-linux-x86_64-4.0.1.tgz)
	mv /usr/local/mongodb-linux-x86_64-4.0.1/* /usr/local/mongodb/(移动后可以删除文件夹rm mongodb-linux-x86_64-4.0.1)


## 4、mongodb.conf（这个文件是没有的，自己创建需要自己创建并且放在/usr/local/mongodb/bin/目录下） ##

	cd ./mongodb/bin/
	vim mongodb.conf（如何添加详细不写，用notepad++添加配置文件，如下文本）
	dbpath=/usr/local/mongodb/data/db #数据文件存放目录
	logpath=/usr/local/mongodb/log/mongodb.log #日志文件存放目录
	port=27017 #端口，默认27017，可以自定义
	logappend=true #开启日志追加添加日志
	fork=true #以守护程序的方式启用，即在后台运行
	bind_ip=0.0.0.0 #默认是127.0.0.1,开启远程访问
	#auth=true（这项暂时不动，因为涉及到auth认证，调试好所有的mongodb的问题后在来弄权限


## 5、添加mongodb环境 ##

	cd /etc/profile
	
	在文件最后一行添加：
	export MONGODB_HOME=/usr/local/mongodb
	export PATH=$PATH:$MONGODB_HOME/bin
	
	source /etc/profile（立即生效）


## 6、启动mongodb ##

	cd /usr/local/mongodb/bin/
	mongod --config mongodb.conf


## 7、开机自动启动mongodb ##

	编辑/etc/rc.d/rc.local,在文件后面加上如下这行：/usr/local/mongodb/bin/mongod --config /usr/local/mongodb/bin/mongodb.conf