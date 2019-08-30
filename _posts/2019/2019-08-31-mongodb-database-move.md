---
layout: post
title: MONGODB导出与导入远程LINUX服务器上的数据
category: Linux
tags: [Linux]
excerpt: MONGODB导出与导入远程LINUX服务器上的数据
---

## 场景 ##

将远程服务器A上的MongoDB数据库test下的集合people导入到服务器B数据库test的集合people_test下。

## 简单方案 ##

先将A服务器数据导出，然后再执行导入到B服务器。

下面的导入和导出操作，均是在git bash下执行，如果是在windows命令行下需要稍微更改路径。

## 工具 ##

利用本地原生MongoDB安装目录下的bin目录中的mongoexport和mongoimport

## 导出数据 ##

首先，进入到MongoDB的安装目录，然后：

	cd bin
	mongoexport -u admin -p 123456 --authenticationDatabase admin -h 10.5.10.22:27017 -d test -c people -o /e/temp/people.json


|  参数   | 说明  | 
|  ----  | ----  |
| -u  | 用户名 |
| -p  | 密码 |
| --authenticationDatabase  | 保存用户凭据的数据库(一般是admin) |
| -h  | host:port |
| -d  | 数据库名 |
| -c  | 表名（只能接受一个表名参数，不能接受由空格、逗号等 分隔的多个表名，也不能用"*"） | 
| -o  | 导出的文件名 |
| --file  | 导入的文件名 |
| --upsert  | 导入的记录创建或更新 |


### 导入数据 ###

也是在bin目录下；

	mongoimport -u admin -p 123456 --authenticationDatabase admin -h 10.6.22.12:27017 -d test -c people_test --file /e/temp/people.json --upsert rm /e/temp/people.json

