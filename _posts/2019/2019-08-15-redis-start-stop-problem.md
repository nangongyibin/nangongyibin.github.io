---
layout: post
title: Redis的启动和停止问题
category: Linux
tags: [Linux]
excerpt: Redis的启动和停止问题
---


## 问题一 ##

Linux启动redis

提示 /var/run/redis_6379.pid exists, process is already running or crashed

问题：

解决方法：

	进入/var/run/文件夹
	执行：rm -f redis_6379.pid
	再次执行启动命令即可


## 问题二 ## 

Redis服务停止(NOAUTH Authentication required)

问题:

解决方法：

	修改redis服务脚本，加入如下所示的红色授权信息即可：
	
	vi /etc/init.d/redis
	
	$CLIEXEC -a "password" -p $REDISPORT shutdown
