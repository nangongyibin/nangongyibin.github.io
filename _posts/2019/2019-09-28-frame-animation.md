---
layout: post
title: Android中动画----帧动画
category: Other
tags: [Other]
excerpt: Android中动画----帧动画
---

## 动画分类：1补间动画、2属性动画、3帧动画  ##

## 代码实现过程: ##

### 在res/drawable目录下创建一个动画资源 ###

        
    <?xml version="1.0" encoding="utf-8"?>
	<animation-list xmlns:android="http://schemas.android.com/apk/res/android">
	    <item android:drawable="@mipmap/girl_1"
	        android:duration="200"/>
	    <item android:drawable="@mipmap/girl_2"
	        android:duration="200"/>
	    <item android:drawable="@mipmap/girl_3"
	        android:duration="200"/>
	    <item android:drawable="@mipmap/girl_4"
	        android:duration="200"/>
	    <item android:drawable="@mipmap/girl_5"
	        android:duration="200"/>
	    <item android:drawable="@mipmap/girl_6"
	        android:duration="200"/>
	    <item android:drawable="@mipmap/girl_7"
	        android:duration="200"/>
	    <item android:drawable="@mipmap/girl_8"
	        android:duration="200"/>
	    <item android:drawable="@mipmap/girl_9"
	        android:duration="200"/>
	    <item android:drawable="@mipmap/girl_10"
	        android:duration="200"/>
	    <item android:drawable="@mipmap/girl_11"
	        android:duration="200"/>
	</animation-list>


### mainActivity页面代码逻辑 ###

    
        
    
        mIv.setBackgroundResource(R.drawable.animation);
        AnimationDrawable animation = (AnimationDrawable) mIv.getBackground();
        animation.run();
	//        animation.start();






