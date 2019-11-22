---
layout: post
title: 使用sql语言操作数据库里面的表
category: MySql
tags: [MySql]
excerpt: 使用sql语言操作数据库里面的表
---

## 1、创建表 ##

    语句: create table 表名称 ( 
	字段 类型(长度), 
	字段 类型(长度) 
	) stuNo not null 唯一 
	示例：创建表 user，字段 id username password sex 
	create table info(id int,name varchar(20),age int); 
	create table info2(id int primary key ,name varchar(20),age int); 

## 2、展示数据库中一共有多少个表 ##

    show tables;


##3、mysql中数据类型 ##

### 字符串型 ###

	VARCHAR、CHAR 
	当创建表时候，使用字符串类型，name varchar(40)，指定数据的长度 
	varchar和char的区别: 
	varchar的长度是可变的 变长 20 zhangsan 
	char的长度是固定的 定长 20 zhangsan+12个空格 

###  大数据类型  ###

	BLOB(存音频，视频，图片等)、TEXT(存字符类型，文本文件) 
	使用这个类型可以存储文件，一般开发，不会直接把文件存到数据库里面，存视频的路径。

### 数值型  ###

	mysql中 TINYINT SMALLINT INT BIGINT FLOAT DOUBLE 
	Java中 byte short int long float double 

### 逻辑性 ###

	BIT 占1位，1字节占8位 
	类似java里面的boolean ​

### 日期型 ###

	DATE：用于表示日期 1945-08-15 
	TIME：用于表示时间 19:10:40 

## 4、查询表的结构 ##

	desc + 表名称 desc info; 
	mysql的约束
	第一种，非空约束 not null表示数据不能为空
	第二种，唯一性约束 unique表中的记录不能重复的
	第三种，主键约束 primary key 表示非空，唯一性，自动增长 
	auto_increment，一旦字段设置为主键，那么该字段就是非空并且唯一

## 5、删除表  ##

	drop + table + 表名称 drop table info;

## 6、使用sql操作表里面的记录  ##

### 往表里面添加记录 ###

    语句：insert into 要添加的表名称 values(要添加的值); 
	示例: insert into info values(2,’zhangsan’,17); 

### 查询表里面的数据 ###

	语句：select 要查询的字段的名称 （*） from 表名称 where 条件 
	示例：select id,name,age from info; select * from info;

### 修改表里面的记录 ###

	语句：update 表名称 set 要修改的字段的名称1=修改的值2,要修改的字段的名称2=修改的值2 where 条件 
	示例：update info set age = 27 where id =1;  

### 删除表里面的记录 删除记录 delete ###

	语句：delete from 表名称 where 条件 
	示例：delete from info where id=2; 删除记录 如果不加where条件代表删除所有的 

### 去除重复的记录 去除重复记录 distinct ###

	语句：select distinct * from 表名; 
	示例：select distinct * from info;

## 7、where语句的使用  ##

	创建一张学生表 
	create table student(id int primary key,name varchar(20),english int,math int);
	往学生表里面添加几条记录 
	insert into student values(1, “aa”,100,80); 
	insert into student values(2, “bb”,80,90); 
	insert into student values(3, “aba”,70,80); 
	查询表里面英语成绩大于 80 
	select * from student where english > 80; 
	查询表里面英语成绩是80 100的学生信息 
	select * from student where english in(80,100); in里面有谁就查询谁 
	查询表里面英语成绩是70，并且数学成绩是80的学生信息 
	select * from student where english = 70 and math=80; 
	查询英语成绩是70~100之间的值 
	select * from student where english >= 70 and english <=100; 
	模糊查询 like 
	select * from student where name like ‘%a%’;
	order by使用 
	根据英语成绩 升序 
	select * from student order by english asc; 默认升序 
	根据英语成绩 降序 desc 
	select * from student order by english desc;

## 8、sql中的函数 (聚合函数) ##

    统计记录数    count
	select count(*) from student; 
	算出英语成绩总和 sum 
	select sum(math) from student; 
	算出英语成绩平均分 avg 总分/数量 
	select sum(english)/count(*) from student; 
	select avg(english) from student; 
	算出最大值 max 
	select max(english) from student; 
	算出最小值 min 
	select min(english) from student;

## 9、分组操作 group by ##

	创建订单表 
	create table orders (id int,name varchar(40),price int); 
	insert into orders values(1,’电视’,2000); 
	insert into orders values(2,’电视’,2000); 
	insert into orders values(3,’苹果’,10); 
	insert into orders values(4,’手机’,500); 
	insert into orders values(5,’手机’,500); 
	insert into orders values(6,’鼠标’,33); 
	insert into orders values(7,’鼠标’,33); 
	统计orders表里面每类商品的总的价格 
	select name,sum(price) from orders group by name; 
	对商品进行分类，得到每类商品的总价格大于66的商品 where关键字后面不可以加聚合函数 
	select name,sum(price) from orders group by name having sum(price)>66;

## 10、limit ##

limit 0 2： 0代表从第几条开始查，2代表查询的个数。