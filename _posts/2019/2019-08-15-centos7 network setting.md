---
layout: post
title: centos7网络设置
category: Linux
tags: [Linux]
excerpt: centos7网络设置
---

## 1、连接以太网(Ethernet) ##


	    # Minimal ISO，安装时没有设置网络，安装后ifconfig不可用
	
		cd /etc/sysconfig/network-scripts       # 只有ifcfg-enp0s25、ifcfg-lo
	
		# 添加IP、掩码、网关等
		vi ifcfg-enp0s25
		
		# IPADDR=192.168.*.*
		# NETMASK=255.255.255.0
		# GATEWAY=192.168.*.*
		# BOOTPROTO=static          # 设为dhcp则为动态获取ip
		# ONBOOT=yes                # 开机启用
		
		# 添加dns服务器
		vi /etc/resolv.conf
		
		# nameserver 180.76.76.76
		# nameserver 114.114.114.114
		
		# 启动/停止/重启网络服务，两种方法等同。注：连接后，stop并未停止连接，原因未知
		/etc/init.d/network stop/start/restart      # Stopping network (via systemctl): [OK]
		service network stop/start/restart
		
		# 测试
		ping www.baidu.com


参考网站：

<https://blog.csdn.net/u014711094/article/details/79832259>