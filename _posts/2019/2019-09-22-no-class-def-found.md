---
layout: post
title: java.lang.NoClassDefFoundError；failed resolution of ；Lorg/apache/http/ProtocolVersion
category: Other
tags: [Other]
excerpt: java.lang.NoClassDefFoundError；failed resolution of ；Lorg/apache/http/ProtocolVersion
---

解决方式：

	在AndroidManifest.xml文件的application标签里面加入

	<uses-library android:name="org.apache.http.legacy" android:required="false" />




参考网址：

<https://blog.csdn.net/u012013969/article/details/92848279>