---
layout: post
title: nginx安装错误
category: Linux
tags: [Linux]
excerpt: nginx的安装
---
### 问题一 ###

执行命令： 

    make && make install

提示错误： 

    cp: ‘conf/koi-win’ and ‘/usr/local/software/nginx/conf/koi-win’ are the same file make[1]: *** [install] Error 1 make[1]: Leaving directory `/usr/local/software/nginx' make: *** [install] Error 2


原因：

解决方法：

    将这一步改一下

	./configure --prefix=/usr/local/nginx
	
	TO
	
	./configure --prefix=/usr/local/nginx --conf-path=/usr/local/nginx/nginx.conf

参考网站：

https://www.jianshu.com/p/9227f0d3d005