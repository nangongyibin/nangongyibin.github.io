---
layout: post
title: 使用sql对数据库进行操作
category: MySql
tags: [MySql]
excerpt: 使用sql对数据库进行操作
---

## 1、首先安装mysql ##

## 2、连接数据库 ##

打开cmd窗口，使用命令，连接mysql数据库 

命令：

    mysql -uroot -p

## 3、查看所有的数据库   ##


语句：

    show databases;

## 4、创建数据库 ##

语句：create database 数据库的名称; 

示例：

    create database ngyb;

## 5、删除数据库 ##

语句：drop database 要删除的数据库的名称; 

示例：

    drop database ngyb; 

## 6、数据库切换 ##

如果想要创建一个数据库表，这个表要在一个数据库里面，所以需要切换到数据库
 
语句：use 要切换的数据库的名称; 

示例：

	use ngyb;

## 7、查看当前使用的数据库 ##

语句：

    select database();