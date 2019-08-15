---
layout: post
title: nginx启动错误
category: Linux
tags: [Linux]
excerpt: nginx的安装
---
### 问题一 ###

启动nginx服务： 

    service nginx start

提示错误： 

    Failed to start SYSV: Nginx is an HTTP(S) server, HTTP(S) reverse


原因：/usr/local/nginx/sbin/nginx来启动了nginx

解决方法：找到这个进程kill掉以后,再执行/etc/rc.d/init.d/nginx start就一切正常了

参考网站：

https://www.cnblogs.com/taui/p/6197045.html