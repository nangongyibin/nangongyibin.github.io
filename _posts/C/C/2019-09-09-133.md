---
layout: post
title: Libcurl编译时问题（一） 
category: C
tags: [C]
excerpt: Libcurl编译时问题（一）  
---

在编译的时候出现问题如下：

	1> LibcurlHtpp.obj：错误LNK2019：无法解析的外部符号_ imp _ curl _ formadd，该符号在函数_ main中被引用
	1> LibcurlHtpp.obj：错误LNK2019：无法解析的外部符号__imp__curl_formfree，该符号在函数__main主中被引用
	1> LibcurlHtpp.obj：错误LNK2019：无法解析的外部符号_ imp _ curl _ global _ init，该符号在函数_main中被引用
	1>LibcurlHtpp.obj : error LNK2019: 无法解析的外部符号 __imp__curl_slist_append，该符号在函数 _main 中被引用
	1>LibcurlHtpp.obj : error LNK2019: 无法解析的外部符号 __imp__curl_slist_free_all，该符号在函数 _main 中被引用
	1>LibcurlHtpp.obj : error LNK2019: 无法解析的外部符号 __imp__curl_easy_strerror，该符号在函数 _main 中被引用
	1>LibcurlHtpp.obj : error LNK2019: 无法解析的外部符号 __imp__curl_easy_init，该符号在函数 _main 中被引用
	1>LibcurlHtpp.obj : error LNK2019: 无法解析的外部符号 __imp__curl_easy_setopt，该符号在函数 _main 中被引用
	1>LibcurlHtpp.obj : error LNK2019: 无法解析的外部符号 __imp__curl_easy_perform，该符号在函数 _main 中被引用
	1>LibcurlHtpp.obj : error LNK2019: 无法解析的外部符号 __imp__curl_easy_cleanup，该符号在函数 _main 中被引用
	1>D:\WorkSpace\C\FileUpload\Debug\FileUpload.exe : fatal error LNK1120: 10 个无法解析的外部命令

解决方案：

	1、给工程添加依赖的库：项目->属性->链接器->输入->附加依赖项，把libcurl.lib ws2_32.lib winmm.lib wldap32.lib添加进去 
	注意，debug配置用libcurld.lib 
	2、加入预编译选项：项目->属性->c/c++ ->预处理器->预处理器，把 ;BUILDING_LIBCURL;HTTP_ONLY复制进去（注意不要丢了”;”）