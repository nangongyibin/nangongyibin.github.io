---
layout: post
title: ERROR 1010 (HY000): Error dropping database (can't rmdir './myapp', errno: 39)
category: Linux
tags: [Linux]
excerpt: ERROR 1010 (HY000): Error dropping database (can't rmdir './myapp', errno: 39)
---

删除数据时

提示错误：

	ERROR 1010 (HY000): Error dropping database (can't rmdir './ahte', errno: 39)

原因：

	已知是文件损坏，导致数据库无法识别

解决方式：

	
	cd /data/mysql/mysql3318/data/ahte
	
	rm -f *


参考网址：

<https://blog.csdn.net/u012349696/article/details/77936997>


