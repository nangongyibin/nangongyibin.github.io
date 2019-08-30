---
layout: post
title: Mongodb基本操作
category: Linux
tags: [Linux]
excerpt: Mongodb基本操作
---
## 1、创建数据并创建用户 ##

### ①、连接MongoDB并访问 ###

	/usr/local/mongodb/bin/mongo
### ②、创建数据库 ###
	use DATABASE_NAME
### ③、查看所有数据库 ###
	show dbs
	刚创建的数据库并不在数据库的列表中， 要显示它，我们需要向数据库插入一些数据。
	db.test.insert({id:1})
### ④、创建mongoDB中的admin账户 ###
	db.createUser({user:"nim",pwd: "nim",roles:[{role:"dbAdmin",db: "nim"} ]})
### ⑤、认证创建的用户 ###
	db.auth('nim', 'nim')      //1代表成功 0代表失败
### ⑥、修改配置文件，使得再次连接数据库需要输入密码(放开红色的部分) ###
	dbpath=/usr/local/mongodb/data/db #数据文件存放目录
	
	logpath=/usr/local/mongodb/log/mongodb.log #日志文件存放目录
	
	port=27017 #端口，默认27017，可以自定义
	
	logappend=true #开启日志追加添加日志
	
	fork=true #以守护程序的方式启用，即在后台运行

	#bind_ip=0.0.0.0 #默认是127.0.0.1,开启远程访问
	#bindIpAll:true
	bind_ip=0.0.0.0
	auth=true #（这项暂时不动，因为涉及到auth认证，调试好所有的mongodb的问题后在来弄权限）
### ⑦、重启Mongodb ###
	查询进程
	Ps -ef | grep mongodb
	杀死已经存在的mongodb进程
	Kill -9 pid
	重启Mongodb
	/usr/local/mongodb/bin/mongod --config /usr/local/mongodb/bin/mongodb.conf
