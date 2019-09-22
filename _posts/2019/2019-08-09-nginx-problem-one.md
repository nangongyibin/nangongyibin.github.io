---
layout: post
title: nginx启动错误
category: Linux
tags: [Linux]
excerpt: nginx启动错误
---
### 问题一 ###

启动nginx服务： 

    service nginx start

提示错误： 

    Failed to start SYSV: Nginx is an HTTP(S) server, HTTP(S) reverse


原因：/usr/local/nginx/sbin/nginx来启动了nginx

解决方法：找到这个进程kill掉以后,再执行/etc/rc.d/init.d/nginx start就一切正常了

参考网站：

<https://www.cnblogs.com/taui/p/6197045.html>

### 问题二 ###

启动nginx服务： 

    service nginx start


问题描述：

	/bin/sh^M: bad interpreter: No such file or directory

原因：拷贝文件从window到linux，编码格式不一样导致的

解决方法：

	使用vi修改文件format
	命令：set ff=unix

### 问题三 ###

启动nginx服务： 

    service nginx start


问题描述：

	一直无响应

原因：

解决方法：

	1、在/etc/init.d/目录下编写脚本，名为nginx
	
	
	#!/bin/sh 
	# 
	# nginx - this script starts and stops the nginx daemon 
	# 
	# chkconfig:   - 85 15 
	# description: Nginx is an HTTP(S) server, HTTP(S) reverse \ 
	#               proxy and IMAP/POP3 proxy server 
	# processname: nginx 
	# config:      /etc/nginx/nginx.conf 
	# config:      /etc/sysconfig/nginx 
	# pidfile:     /var/run/nginx.pid 
	
	# Source function library. 
	. /etc/rc.d/init.d/functions 
	
	# Source networking configuration. 
	. /etc/sysconfig/network 
	
	# Check that networking is up. 
	[ "$NETWORKING" = "no" ] && exit 0 
	
	nginx="/usr/local/nginx/sbin/nginx" 
	prog=$(basename $nginx) 
	
	NGINX_CONF_FILE="/usr/local/nginx/conf/nginx.conf" 
	
	[ -f /etc/sysconfig/nginx ] && . /etc/sysconfig/nginx 
	
	lockfile=/var/lock/subsys/nginx 
	
	start() { 
	    [ -x $nginx ] || exit 5 
	    [ -f $NGINX_CONF_FILE ] || exit 6 
	    echo -n $"Starting $prog: " 
	    daemon $nginx -c $NGINX_CONF_FILE 
	    retval=$? 
	    echo 
	    [ $retval -eq 0 ] && touch $lockfile 
	    return $retval 
	} 
	
	stop() { 
	    echo -n $"Stopping $prog: " 
	    killproc $prog -QUIT 
	    retval=$? 
	    echo 
	    [ $retval -eq 0 ] && rm -f $lockfile 
	    return $retval 
	killall -9 nginx 
	} 
	
	restart() { 
	    configtest || return $? 
	    stop 
	    sleep 1 
	    start 
	} 
	
	reload() { 
	    configtest || return $? 
	    echo -n $"Reloading $prog: " 
	    killproc $nginx -HUP 
	RETVAL=$? 
	    echo 
	} 
	
	force_reload() { 
	    restart 
	} 
	
	configtest() { 
	$nginx -t -c $NGINX_CONF_FILE 
	} 
	
	rh_status() { 
	    status $prog 
	} 
	
	rh_status_q() { 
	    rh_status >/dev/null 2>&1 
	} 
	
	case "$1" in 
	    start) 
	        rh_status_q && exit 0 
	    $1 
	        ;; 
	    stop) 
	        rh_status_q || exit 0 
	        $1 
	        ;; 
	    restart|configtest) 
	        $1 
	        ;; 
	    reload) 
	        rh_status_q || exit 7 
	        $1 
	        ;; 
	    force-reload) 
	        force_reload 
	        ;; 
	    status) 
	        rh_status 
	        ;; 
	    condrestart|try-restart) 
	        rh_status_q || exit 0 
	            ;; 
	    *)    
	      echo $"Usage: $0 {start|stop|status|restart|condrestart|try-restart|reload|force-reload|configtest}" 
	        exit 2 
	
	esac  
	
	2、开启nginx服务
	
	cp nginx /etc/init.d/
	chmod 755 /etc/init.d/nginx
	chkconfig --add nginx

	3、nginx启动，停止，无间隔重启
	
	service nginx start
	service nginx stop
	service nginx configtest
	service nginx reload

参考网址：

<https://blog.csdn.net/baidu_37895884/article/details/78218322>


### 问题四 ###

启动nginx服务： 

    service nginx start


问题描述：

	centOS7访问nginx失败解决-.0:80 failed (98: Address already in use)解决

原因：

解决方法：

	[root@localhost ~]# killall -9 nginx
	再次启动nginx：
	[root@localhost ~]# service nginx start
	查看是否启动：
	[root@localhost ~]# ps aux|grep nginx
	输出：
	root       7110  0.0  0.0  24348   752 ?        Ss   22:32   0:00 nginx: master process /usr/local/nginx/sbin/nginx
	nobody     7111  0.0  0.0  26860  1508 ?        S    22:32   0:00 nginx: worker process
	root       7114  0.0  0.0 112664   968 pts/0    S+   22:33   0:00 grep --color=auto nginx
	启动成功！
	访问nginx
	在浏览器地址栏输入你的Linux虚拟机的静态ip，会跳转到nginx的欢迎页面。


参考网址：

<https://blog.csdn.net/zyhlearnjava/article/details/71908529>
