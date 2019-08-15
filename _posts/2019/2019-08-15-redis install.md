---
layout: post
title: Redis的安装
category: Linux
tags: [Linux]
excerpt: Redis的安装
---

## 1、安装必需包gcc ##


	yum install gcc


## 2、下载redis,并解压 ##

	wget http://download.redis.io/releases/redis-5.0.5.tar.gz
	tar zxvf redis-5.0.5.tar.gz


## 3、进入redis解压目录，编译安装 ##

	cd redis-5.0.5
	#如果不加参数,linux下会报错
	make MALLOC=libc



## 4、将/usr/local/redis-5.0.5/src目录下的文件加到/usr/local/bin目录 ##

	在解压目录下执行：cd src && make install


## 5、启动redis ##

	直接启动方式，在redis解压目录的src文件夹下执行：
	./redis-server
	
![](http://www.nangongyibin.com/assets/images/redis1.png)
 
	如上图：redis启动成功，但是这种启动方式需要一直打开窗口，不能进行其他操作，不太方便。
	按 ctrl + c可以关闭窗口
	以后台进程方式启动redis
	修改redis.conf文件，该文件在redis解压目录下
	vi redis.conf
	#将daemonize no 改为daemonize yes
	指定redis.conf文件启动
	./redis-server /usr/local/redis-5.0.5/redis.conf

![](http://www.nangongyibin.com/assets/images/redis2.png)

	关闭redis进程
	#查看当前redis进程
	ps -aux | grep redis
	#使用kill命令杀死进程
	kill -9 pid