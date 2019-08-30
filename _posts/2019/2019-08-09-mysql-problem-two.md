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

### 问题四 ###


登录mysql服务：

    mysql -uroot -p

提示错误：

    ERROR 1862 (HY000): Your password has expired. To log in you must change it using a client that supports expired passwords.

原因：密码过期

解决方法：

1、修改/etc/my.cnf文件，在[mysqld]下加入“skip-grant-tables”。

2、重启mysql服务器

3、登陆mysql

    [root@:vg_adn_tidbCkhsTest /usr/local/src]#mysql -u root -p                   #此处直接按下enter键即可
	Enter password: 
	Welcome to the MariaDB monitor.  Commands end with ; or \g.
	Your MySQL connection id is 2
	Server version: 5.7.24 MySQL Community Server (GPL)
	
	Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.
	
	Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
	
	MySQL [(none)]> update mysql.user set password_expired='N' where user='root'
	    -> ;
	Query OK, 1 row affected (0.00 sec)
	Rows matched: 1  Changed: 1  Warnings: 0
	
	MySQL [(none)]> flush privileges;
	Query OK, 0 rows affected (0.00 sec)
	
	MySQL [(none)]> exit

4、修改/etc/my.cnf。把“skip”这一行内容注释掉

5、再次重启mysql服务器即可


### 问题五 ###


登录mysql服务：

    mysql -uroot -p

提示错误：

    ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)

原因：tmp目录无mysql.sock文件

解决方法：

	搜索mysql.sock文件，发现在/var/lib/mysql/mysql.sock
	建立一个软连接	
	ln -s /var/lib/mysql/mysql.sock /tmp/mysql.sock

参考网址：

<https://blog.csdn.net/a1173537204/article/details/88069724>