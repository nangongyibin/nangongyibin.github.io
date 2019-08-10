---
layout: post
title: nginx的安装
category: Linux
tags: [Linux]
excerpt: nginx的安装
---
### 1、安装必要的依赖插件  ###

    yum -y install gcc gcc-c++ autoconf automake libtool make cmake zlib zlib-devel openssl openssl-devel pcre pcre-devel

### 2、下载安装包 (同样如果想安装其他的版本，可以去下面官网链接，选择其他版本的链接进行拷贝替换)  ###

    wget https://nginx.org/download/nginx-1.16.0.tar.gz



### 3、解压并安装  ###

    tar zxvf nginx-1.16.0.tar.gz
	cd nginx-1.16.0
	./configure --prefix=/usr/local/nginx
	make && make install


### 4、添加全部命令 ###

    ln -s /usr/local/nginx/sbin/nginx /usr/bin/nginx

### 5、测试安装 ###

	nginx -V


### 6、在linux系统的/etc/init.d/目录下创建nginx文件，使用如下命令 ###

    vi /etc/init.d/nginx
	nginx 脚本内容：
	
	#!/bin/sh
	#
	# nginx - this script starts and stops the nginx daemon
	#
	# chkconfig:   - 85 15
	# description:  NGINX is an HTTP(S) server, HTTP(S) reverse 
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
	nginx="/usr/sbin/nginx"
	prog=$(basename $nginx)
	NGINX_CONF_FILE="/etc/nginx/nginx.conf"
	[ -f /etc/sysconfig/nginx ] && . /etc/sysconfig/nginx
	lockfile=/var/lock/subsys/nginx
	make_dirs() {
	   # make required directories
	   user=`$nginx -V 2>&1 | grep "configure arguments:" | sed 's/[^*]*--user=\([^ ]*\).*/\1/g' -`
	   if [ -z "`grep $user /etc/passwd`" ]; then
	       useradd -M -s /bin/nologin $user
	   fi
	   options=`$nginx -V 2>&1 | grep 'configure arguments:'`
	   for opt in $options; do
	       if [ `echo $opt | grep '.*-temp-path'` ]; then
	           value=`echo $opt | cut -d "=" -f 2`
	           if [ ! -d "$value" ]; then
	               # echo "creating" $value
	               mkdir -p $value && chown -R $user $value
	           fi
	       fi
	   done
	}
	start() {
	    [ -x $nginx ] || exit 5
	    [ -f $NGINX_CONF_FILE ] || exit 6
	    make_dirs
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

注意：
自定义编译安装的nginx，需要根据您的安装路径修改下面这两项配置：
nginx=”/usr/sbin/nginx” 修改成nginx执行程序的路径。
NGINX_CONF_FILE=”/etc/nginx/nginx.conf” 修改成配置文件的路径。



### 7、保存脚本文件后设置文件的执行权限 ###


    chmod a+x /etc/init.d/nginx
	然后，就可以通过该脚本对nginx服务进行管理了：
	/etc/init.d/nginx start
	/etc/init.d/nginx stop


### 8、使用chkconfig进行管理，先将nginx服务加入chkconfig管理列表 ###

    chkconfig --add /etc/init.d/nginx
	加完这个之后，就可以使用service对nginx进行启动，重启等操作了。
	service nginx start
	service nginx stop


### 9、设置终端模式开机启动 ###

    chkconfig nginx on

### 10、验证是否成功 ###

    shutdown -r now