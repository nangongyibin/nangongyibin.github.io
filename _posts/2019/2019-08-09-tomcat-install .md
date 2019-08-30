---
layout: post
title: Tomcat的安装
category: Linux
tags: [Linux]
excerpt: Tomcat的安装
---
### 1、下载tomcat  ###

<http://tomcat.apache.org/>

### 2、将apache-tomcat-8.0.50.tar.gz解压 ###

    tar  -zxvf apache-tomcat-8.0.50.tar.gz

### 3、修改apache-tomcat-8.0.53名字为tomcat8 ###

	mv apache-tomcat-8.0.53/ tomcat8


### 4、进入tomcat下bin目录启动tomcat ###

    cd tomcat/bin
	./startup.sh

### 5、将catalina.sh拷贝到/etc/init.d/（此文件是放什么的大家自行去补脑）下，并重命名为tomcat。 ###

    cd /usr/local/software/tomcat9
	cd bin
	cp catalina.sh /etc/init.d/tomcat
	cd /etc/init.d/	

### 6、文件拷贝完成后，对tomcat文件进行编辑，vim tomcat打开tomcat文件，并按i进行插入编辑，如下图，编辑完成后保存退出。 ###

![](http://www.nangongyibin.com/assets/images/tomcat1.png)

### 7、添加tomcat为系统服务 ###

未添加tomcat为系统服务之前，查看系统服务chkconfig --list，发现并没有tomcat服务，如下图

![](http://www.nangongyibin.com/assets/images/tomcat2.png)

添加文件可执行权限，然后添加tomcat为系统服务，如下图

![](http://www.nangongyibin.com/assets/images/tomcat3.png)


执行命令chkconfig --list,如下图

![](http://www.nangongyibin.com/assets/images/tomcat4.png)

### 8、启动和关闭服务 ###

启动服务，并用浏览器访问，如下图

![](http://www.nangongyibin.com/assets/images/tomcat5.png)

关闭服务，与关闭其他的系统服务一样，如下图

![](http://www.nangongyibin.com/assets/images/tomcat6.png)

### 9、设置tomcat服务随系统启动而自启动（设置成系统自启动服务） ###

    直接在/etc/rc.local文件最后添加语句/usr/local/tomcat7/bin/startup.sh，重启系统，运行ps -ef|grep java,出现如下信息，则说明tomcat服务自启动了！

![](http://www.nangongyibin.com/assets/images/tomcat7.png)

当然tomcat设置自启动，重启系统后，最直白验证tomcat启动了的方式其实是直接访问tomcat猫就可以了，出现如下可爱的猫，那么tomcat随系统自启动了！