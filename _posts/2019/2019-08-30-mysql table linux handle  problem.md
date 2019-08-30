---
layout: post
title: 向数据库表插入数据遇到的问题
category: MySql
tags: [MySql]
excerpt: 向数据库表插入数据遇到的问题
---

向数据库表插入数据： 

    insert into orders values(1,'电视',2000);

提示错误： 

    ERROR 1366 (HY000): Incorrect string value: '\xE7\x94\xB5\xE8\xA7\x86' for column 'name' at row 1


原因：

解决方法：把表默认的字符集和所有字符列（CHAR,VARCHAR,TEXT）改为新的字符集：

	LTER TABLE tbl_name CONVERT TO CHARACTER SET character_name [COLLATE ...]
	如：ALTER TABLE orders CONVERT TO CHARACTER SET utf8 COLLATE utf8_general_ci;