---
layout: post
title: mysql连接问题及导入导出问题
category: Linux
tags: [Linux]
excerpt: mysql连接问题及导入导出问题
---
### 问题一 ###

Navicat连Mysql数据库出现如下的错误

提示错误： 

    2013-Lost connection to MYSQL server at 'waiting for initial communication packet',system error：0


原因：

解决方法：

    打开my.cnf，找到[mysqld]项，在其后加入一句：skip-name-resolve，保存，重启mysql服务即可~


### 问题二 ###

Navicat连Mysql数据库出现如下的错误

提示错误： 

    1045    Access denied for user 'root'@'localhost' (using password:YES)


原因：

解决方法：

    打开my.cnf，找到[mysqld]项，在其后加入一句：skip-grant-tables，保存，重启mysql服务即可~


### 问题三 ###

拷贝结构及数据遇到的问题

提示错误： 

    1067 - Invalid default value for   timestamp


原因：

解决方法：

    在mysql配置文件中增加配置参数
	[mysqld]节点下添加
	
	explicit_defaults_for_timestamp = ON
	重启mysql数据库使配置生效。

### 问题四 ###

导出数据遇到的问题

提示错误： 

    不能通过当前网络连接数据库，无法导出库（内网连接不了外网数据库，但是可以通过一个内网服务器连接外网服务器数据库）


原因：

解决方法：

    连接上外网服务器后，执行如下的命令
	mysqldump -u用户名 -p密码 数据库名 > 数据库名.sql
	然后将文件拷贝到内网服务器上
	scp /usr/local/tools/xxx文件 root@192.168.0.240:/usr/local/tools
	目标文件                 目的服务器及位置

### 问题五 ###

导入数据遇到的问题

提示错误： 

    ERROR 1273 (HY000): Unknown collation: 'utf8mb4_0900_ai_ci'


原因：
	
	MySQL版本不兼容

解决方法：

    打开sql文件，将文件中的所有
	utf8mb4_0900_ai_ci替换为utf8_general_ci
	utf8mb4替换为utf8
	保存后再次运行sql文件，运行成功
