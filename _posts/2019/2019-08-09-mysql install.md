---
layout: post
title: mysql的安装
category: Linux
tags: [Linux]
excerpt: mysql的安装
---
### 1、检查是否已安装过mariadb，若有便删除（linux系统自带的）  ###

    rpm -qa | grep mariadb
	rpm -e --nodeps mariadb-libs-5.5.44-2.el7.centos.x86_64

### 2、检查是否已安装过mysql，若有便删除（linux系统自带的）  ###

    rpm -qa | grep mariadb
	rpm -e --nodeps mariadb-libs-5.5.44-2.el7.centos.x86_64



### 3、检查mysql组和用户是否存在，如无创建  ###

    cat /etc/group | grep mysql
	cat /etc/passwd |grep mysql
	groupadd mysql
	useradd -r -g mysql mysql

### 4、从官网下载mysql安装包，解压后移动到/usr/local/mysql下 ###

    tar xzvf mysql-5.7.24-linux-glibc2.12-x86_64.tar.gz
	mv mysql-5.7.24-linux-glibc2.12-x86_64 /usr/local/mysql

### 5、在mysql下添加data目录 ###

	mkdir /usr/local/mysql/data


### 6、更改mysql目录下所有的目录及文件夹所属组合用户 ###

    cd /usr/local/ 
	chown -R mysql:mysql mysql/
	chmod -R 755 mysql/


### 7、编译安装并初始化mysql，记住命令行末尾的密码 ###


    /usr/local/mysql/bin/mysqld --initialize --user=mysql --datadir=/usr/local/mysql/data --basedir=/usr/local/mysql

### 8、启动mysql服务 ###

    /usr/local/mysql/support-files/mysql.server start

### 9、做个软连接，重启服务 ###

    ln -s /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql 
	service mysql restart

### 10、做个软链接，将安装目录下的mysql 放在/usr/bin 目录下 ###

    ln -s /usr/local/mysql/bin/mysql /usr/bin


### 11、登录msyql，输入密码（密码为步骤7初始化生成的密码） ###

    mysql -u root -p
	Enter password:

### 12、修改密码并开放远程 ###

    msql>alter user 'root'@'localhost' identified by '123456';
	mysql>use mysql;
	msyql>update user set user.Host='%' where user.User='root';
	mysql>flush privileges;
	mysql>quit

### 13、编辑my.cnf，添加配置文件，配置内容为 ###


    vi /usr/local/mysql/my.cnf

	[mysqld]
	port = 3306
	sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES


### 14、设置开机自启动 ###


    1、将服务文件拷贝到init.d下，并重命名为mysql
	cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysqld
	2、赋予可执行权限
	chmod +x /etc/init.d/mysqld
	3、添加服务
	chkconfig --add mysqld
	4、显示服务列表
	chkconfig --list
	5、重启服务器
	reboot
