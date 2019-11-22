---
layout: post
title: Sql异常
category: MySql
tags: [MySql]
excerpt: Sql异常
---

## 问题一 ##

JAVA操作数据时


提示错误： 

    com.mysql.jdbc.exceptions.MySQLSyntaxErrorException: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'order' at line 1


原因：

解决方法：

	如果你用了mysql中的关键字做字段，当你查询的时候可以用  `order` 来括起来，这个 ` 并不是单引号，而是数字那一行键的最左边的那个键，在英文状态下的才为 ` ，用它把关键字括起来就可以解决这个问题。


 