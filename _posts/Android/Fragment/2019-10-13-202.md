---
layout: post
title:    Fragment介绍   
category: Fragment
tags: [Fragment]
excerpt:  Fragment介绍  
---


## Fragment总是被嵌入到Activity里,Fragment要添加到ViewGroup里 ##
 
## Fragment是在android3.0的时候被引入的  ##


## 代码实现 ##


### 在布局声明 ###
    

	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    xmlns:app="http://schemas.android.com/apk/res-auto"
	    xmlns:tools="http://schemas.android.com/tools"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent"
	    android:orientation="vertical"
	    tools:context=".MainActivity">
	
	    <fragment
	        android:id="@+id/fm1"
	        android:layout_width="match_parent"
	        android:layout_height="0dp"
	        android:layout_weight="1"
	        android:name="com.ngyb.fm.OneFragment"/>
	
	    <fragment
	        android:id="@+id/fm2"
	        android:layout_width="match_parent"
	        android:layout_height="0dp"
	        android:layout_weight="1"
	        android:name="com.ngyb.fm.TwoFragment"/>
	</LinearLayout>


### 声明Fragment 需要重写onCreateView方法  ###

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_two, null);
    }