---
layout: post
title:   滚动条 viewPager 
category: Layout
tags: [Layout]
excerpt:  滚动条 viewPager
---


## [1]在布局中声明控件 ##

    <androidx.viewpager.widget.ViewPager
        android:id="@+id/vp"
        android:layout_width="match_parent"
        android:layout_height="250dp" />

## [2]viewpager展示数据和listview一样需要一个适配器(pagerAdapter) 定义适配器 ##

    class MyPagerAdapter extends PagerAdapter {

        @Override
        public int getCount() {
            return vpMax;
        }

        @Override
        public boolean isViewFromObject(@NonNull View view, @NonNull Object object) {
            return view == object;
        }


        @NonNull
        @Override
        public Object instantiateItem(@NonNull ViewGroup container, int position) {
            position = position % imageResId.length;
            ImageView imageView = list.get(position);
            container.addView(imageView);
            return imageView;
        }

        @Override
        public void destroyItem(@NonNull ViewGroup container, int position, @NonNull Object object) {
            container.removeView((View) object);
        }
    }

## [3]添加小圆点和文本对应的布局 ##

	<?xml version="1.0" encoding="utf-8"?>
	<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent">
	
	    <androidx.viewpager.widget.ViewPager
	        android:id="@+id/vp"
	        android:layout_width="match_parent"
	        android:layout_height="250dp" />
	
	    <LinearLayout
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:layout_alignBottom="@id/vp"
	        android:background="#66000000"
	        android:paddingTop="10dp"
	        android:paddingBottom="10dp">
	
	        <TextView
	            android:id="@+id/tv"
	            android:layout_width="match_parent"
	            android:layout_height="match_parent"
	            android:gravity="center"
	            android:text="耕耘不断，成功在望"
	            android:textColor="#fff"
	            android:textSize="24sp" />
	    </LinearLayout>
	
	    <LinearLayout
	        android:id="@+id/ll"
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:layout_alignBottom="@id/vp"
	        android:gravity="center"
	        android:orientation="horizontal"
	        android:paddingBottom="5dp" />
	</RelativeLayout>


## [4]初始化小圆点的逻辑 ##

    private void initDot() {
        for (int i = 0; i < list.size(); i++) {
            ImageView imageView = list.get(i);
            View view = new View(getApplicationContext());
            LinearLayout.LayoutParams layoutParams = new LinearLayout.LayoutParams(7, 7);
            if (i != 0) {
                layoutParams.leftMargin = 7;
            }
            view.setBackgroundResource(R.drawable.selctor_dot);
            view.setLayoutParams(layoutParams);
            ll.addView(view);
        }
    }

## [5]当滑动viewpager的时候 ,改变小圆点的状态并且还要改变对应文本信息,就是给viewpager设置滑动的监听 ##

        vp.addOnPageChangeListener(new ViewPager.OnPageChangeListener() {
            @Override
            public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) {

            }

            @Override
            public void onPageSelected(int position) {
                changeUI(position);
            }

            @Override
            public void onPageScrollStateChanged(int state) {

            }
        });

## [6]由于改变小圆点的状态和对应文本信息这个逻辑用到了2次，所以抽出一个方法调用 ##

    private void changeUI(int position) {
        position = position % list.size();
        View child = ll.getChildAt(position);
        child.setSelected(true);
        tv.setText(descs[position]);
        if (currentChild != null) {
            currentChild.setSelected(false);
        }
        currentChild = child;
    }

[7]实现无限循环 原理:就是在适配器getcount方法里面返回一个比较大的数 

5 % 5—–>0 

6 %5—–>1 

7 %5—–>2 

…… 
50—->0 

### 适配器getCount方法逻辑 ###

        @Override
        public int getCount() {
            return vpMax;
        }

### 初始化每个条目的业务逻辑 ###

        @NonNull
        @Override
        public Object instantiateItem(@NonNull ViewGroup container, int position) {
            position = position % imageResId.length;
            ImageView imageView = list.get(position);
            container.addView(imageView);
            return imageView;
        }

## [8]实现viewpager自动滚动逻辑 handler 在onStrat方法里面通过handler发消息实现无限循环 ##

    @Override
    protected void onStart() {
        handler.sendEmptyMessageDelayed(10, 3000);
        super.onStart();
    }

## [9]在handlemessage方法里面让viewpager加载下一页 ##

    @SuppressLint("HandlerLeak")
    private Handler handler = new Handler() {
        @Override
        public void handleMessage(Message msg) {
            if (msg.what == 10) {
                vp.setCurrentItem(vp.getCurrentItem() + 1);
                handler.sendEmptyMessageDelayed(10,3000);
            }
            super.handleMessage(msg);
        }
    };