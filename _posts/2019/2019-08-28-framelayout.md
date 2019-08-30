---
layout: post
title: FrameLayout
category: Layout
tags: [Layout]
excerpt: FrameLayout
---

# 1、帧布局：分层展示控件 #

    <?xml version="1.0" encoding="utf-8"?>
	<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent">
	
	    <TextView
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:text="视频" />
	
	    <Button
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content"
	        android:layout_gravity="center"
	        android:text="播放" />
	</FrameLayout>