---
layout: post
title: mysql启动问题
category: Linux
tags: [Linux]
excerpt: mysql启动问题
---

### 问题一 ###

启动mysql服务： 

    /usr/local/software/mysql/support-files/mysql.server start

提示错误： 

    /usr/local/software/mysql/support-files/mysql.server: line 239: my_print_defaults: command not found
	/usr/local/software/mysql/support-files/mysql.server: line 259: cd: /usr/local/mysql: No such file or directory


原因：目录错误

解决方法：修改/usr/local/software/mysql/support-files/mysql.server中的目录/usr/local修改为/usr/local/software

### 问题二 ###

启动mysql服务：

    /usr/local/software/mysql/support-files/mysql.server start

提示错误：

    log-error set to '/var/log/mariadb/mariadb.log', however file don't exists.

原因：权限问题

解决方法：

    mkdir /var/log/mariadb 
	touch /var/log/mariadb/mariadb.log 
	chown -R mysql:mysql  /var/log/mariadb/

### 问题三 ###

启动mysql服务：

    /usr/local/software/mysql/support-files/mysql.server start

提示错误：

    Directory '/var/lib/mysql' for UNIX socket file don't exists.

原因：“var/lib/mysql”目录不存在，首要先创建：

解决方法：

    mkdir   /var/lib/mysql
	chmod 777  /var/lib/mysql

