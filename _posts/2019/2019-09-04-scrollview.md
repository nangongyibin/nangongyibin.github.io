---
layout: post
title: ScrollView
category: Layout
tags: [Layout]
excerpt: ScrollView
---


### scrollView 垂直滚动的view ###

    
    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1">

        <TextView
            android:id="@+id/tv"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />
    </ScrollView>



注意：scrollView控件只能包裹一个孩子，如果想包裹多个在外面套一个布局。



