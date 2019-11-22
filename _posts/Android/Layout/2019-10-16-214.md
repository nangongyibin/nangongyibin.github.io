---
layout: post
title:    下拉列表的实现（一）  
category: Layout
tags: [Layout]
excerpt:  下拉列表的实现（一） 
---


## autoCompleteTextview ##


### [1]在布局中声明 ###

	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    xmlns:app="http://schemas.android.com/apk/res-auto"
	    xmlns:tools="http://schemas.android.com/tools"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent"
	    android:orientation="vertical"
	    tools:context=".MainActivity">
	
	    <AutoCompleteTextView
	        android:id="@+id/actv"
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:completionThreshold="1"
	        android:singleLine="true" />
	</LinearLayout>

### [2]这个控件展示数据原理和listview一样，需要一个适配器，代码如下: ###

    private void initActv() {
        String [] str = {"小周","小青","小成","小闫"};
        mActv = findViewById(R.id.actv);
        mActv.setAdapter(new ArrayAdapter<String>(this,android.R.layout.simple_dropdown_item_1line,str));
    }