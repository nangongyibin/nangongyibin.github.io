---
layout: post
title: RelativeLayout
category: Layout
tags: [Layout]
excerpt: RelativeLayout
---

# 1、相对布局：里面的控件默认都从左上角开始排列 #

    <?xml version="1.0" encoding="utf-8"?>
	<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent">
	
	    <TextView
	        android:id="@+id/tv1"
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content"
	        android:layout_centerVertical="true"
	        android:text="天道酬勤" />
	
	    <Button
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:layout_centerVertical="true"
	        android:layout_toRightOf="@id/tv1"
	        android:text="点一下我" />
	</RelativeLayout>