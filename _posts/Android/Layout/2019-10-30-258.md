---
layout: post
title:   侧滑菜单 
category: Layout
tags: [Layout]
excerpt:  侧滑菜单
---
代码实现步骤

### [1]先画主页面 代码如下 ###


	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent"
	    android:orientation="vertical">
	
	    <LinearLayout
	        android:layout_width="match_parent"
	        android:layout_height="?attr/actionBarSize"
	        android:background="@drawable/top_bar_bg"
	        android:orientation="horizontal">
	
	        <Button
	            android:id="@+id/back"
	            android:layout_width="wrap_content"
	            android:layout_height="match_parent"
	            android:background="@drawable/main_back" />
	
	        <ImageView
	            android:layout_width="wrap_content"
	            android:layout_height="wrap_content"
	            android:background="@drawable/top_bar_divider" />
	
	        <TextView
	            android:layout_width="match_parent"
	            android:layout_height="match_parent"
	            android:gravity="center"
	            android:text="首页"
	            android:textColor="@android:color/white"
	            android:textSize="25sp" />
	    </LinearLayout>
	
	    <TextView
	        android:layout_width="match_parent"
	        android:layout_height="match_parent"
	        android:gravity="center"
	        android:text="天道酬情追梦无疆" />
	</LinearLayout>


### [2]画菜单页面 ###

	<?xml version="1.0" encoding="utf-8"?>
	<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
	    android:layout_width="240dp"
	    android:layout_height="match_parent"
	    android:background="@drawable/menu_bg"
	    android:orientation="vertical">
	
	    <LinearLayout
	        android:background="@drawable/menu_bg"
	        android:layout_width="match_parent"
	        android:layout_height="match_parent"
	        android:layout_gravity="center"
	        android:orientation="vertical">
	        <TextView
	            style="@style/menu_tv_style"
	            android:drawableLeft="@drawable/tab_news"
	            android:text="寻物启事"/>
	
	        <TextView
	            android:drawableLeft="@drawable/tab_focus"
	            android:text="失物招领"
	            style="@style/menu_tv_style" />
	    </LinearLayout>
	</ScrollView>

### [3]把共同的属性抽到一个style里面 ###

    <style name="menu_tv_style">
        <item name="android:layout_width">match_parent</item>
        <item name="android:layout_height">wrap_content</item>
        <item name="android:drawablePadding">15dp</item>
        <item name="android:padding">15dp</item>
        <item name="android:textSize">25sp</item>
        <item name="android:layout_gravity">center</item>
        <item name="android:gravity">center</item>
        <item name="android:textColor">@android:color/white</item>
        <item name="android:textStyle">bold</item>
    </style>

### [4] 通过include 把2个孩子加入到main_activity页面 ###

	<?xml version="1.0" encoding="utf-8"?>
	<com.ngyb.slidingmenu.SlidingMenu xmlns:android="http://schemas.android.com/apk/res/android"
	    xmlns:app="http://schemas.android.com/apk/res-auto"
	    xmlns:tools="http://schemas.android.com/tools"
	    android:id="@+id/sm"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent"
	    tools:context=".MainActivity">
	
	    <include layout="@layout/menu" />
	
	    <include layout="@layout/main" />
	</com.ngyb.slidingmenu.SlidingMenu>

### [5]对孩子重新排版,重写onlayout方法 ###

    @Override
    protected void onLayout(boolean changed, int l, int t, int r, int b) {
        super.onLayout(changed, l, t, r, b);
        View menu = getChildAt(0);
        View main = getChildAt(1);
        width = menu.getMeasuredWidth();
        main.layout(l, t, r, b);
        menu.layout(-width, t, l, b);
    }

### [6]让容器消费事件,就是重写onTouchEvent方法,处理手指按下和移动的逻辑 ###




   	@Override
    public boolean onTouchEvent(MotionEvent event) {
        switch (event.getAction()) {
            case MotionEvent.ACTION_DOWN:
                downX = event.getX();
                break;
            case MotionEvent.ACTION_MOVE:
                currentX = event.getX();
                distanceX = currentX - downX + currentLeft;
                if (distanceX < 0) {
                    distanceX = 0;
                } else if (distanceX > width) {
                    distanceX = width;
                }
                scrollToX((int) distanceX);
                break;
            case MotionEvent.ACTION_UP:
                if (distanceX >= width / 2) {
                    currentLeft = width;
                } else {
                    currentLeft = 0;
                }
                startX = distanceX;
                endX = currentLeft;
                scrollToEnd(startX, endX);
                break;
        }
        return true;
    }

### [7]处理手指抬起的逻辑 ###

            case MotionEvent.ACTION_UP:
                if (distanceX >= width / 2) {
                    currentLeft = width;
                } else {
                    currentLeft = 0;
                }
                startX = distanceX;
                endX = currentLeft;
                scrollToEnd(startX, endX);
                break;


### [8]让view 实现平滑滚动. Scroller  ###

#### [8.1]先获取scroller实例 ####

	scroller = new Scroller(getContext());

#### [8.2] 模拟X轴滚动的数据 ####

    public void scrollToEnd(float startX, float endX) {
        sx = (int) startX;
        dx = (int) (endX - startX);
        time = dx * 15;
        scroller.startScroll(sx, 0, dx, 0, time);
        invalidate();
    }

#### [8.3] 取出模拟的数据 ####

    @Override
    public void computeScroll() {
        if (scroller.computeScrollOffset()) {
            currX = scroller.getCurrX();
            scrollToX(currX);
            invalidate();
        }
    }

### [9].点击按钮实现菜单切换 ###

    public void switchMenu() {
        if (currentLeft == 0) {
            currentLeft = width;
            startX = 0;
        } else {
            currentLeft = 0;
            startX = width;
        }
        scrollToEnd(startX, currentLeft);
    }

### [10].处理事件冲突. 如果x轴移动的距离 > Y轴移动的距离就拦截事件 ###


    /**
     * 事件是否拦截的处理
     * 处理逻辑是：x坐标的移动量大于y坐标的移动量，就把触摸事件拦截掉。
     *
     * @param ev
     * @return
     */
    @Override
    public boolean onInterceptTouchEvent(MotionEvent ev) {
        switch (ev.getMetaState()) {
            case MotionEvent.ACTION_DOWN:
                downX = ev.getX();
                downY = ev.getY();
                break;
            case MotionEvent.ACTION_MOVE:
                moveX = ev.getX() - downX;
                moveY = ev.getY() - downY;
                downX = ev.getX();
                downY = ev.getY();
                if (Math.abs(moveX) > Math.abs(moveY)) {
                    Log.e(TAG, "onInterceptTouchEvent: ");
                    return true;
                }
                break;
            case MotionEvent.ACTION_UP:
                break;
        }
        return false;
    }