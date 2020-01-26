---
layout: post
title:    交叉布局  
category: Layout
tags: [Layout]
excerpt:  交叉布局
---



	package com.ngyb.crossviewgroup;
	
	import android.content.Context;
	import android.util.AttributeSet;
	import android.view.View;
	import android.widget.RelativeLayout;
	
	/**
	 * 作者：南宫燚滨
	 * 描述：
	 * 邮箱：nangongyibin@gmail.com
	 * 日期：2019/10/19 18:21
	 */
	public class CrossLayout extends RelativeLayout {
	    private boolean isLeft = true;
	
	    public CrossLayout(Context context, AttributeSet attrs) {
	        super(context, attrs);
	    }
	
	    @Override
	    protected void onLayout(boolean changed, int l, int t, int r, int b) {
	        int top = 0;
	        int left = 0;
	        int right = 0;
	        int bottom = 0;
	        for (int i = 0; i < getChildCount(); i++) {
	            View view = getChildAt(i);
	            if (isLeft) {
	                if (i % 2 == 0) {
	                    left = 0;
	                } else {
	                    left = getMeasuredWidth() - view.getMeasuredWidth();
	                }
	            } else {
	                if (i % 2 == 0) {
	                    left = getMeasuredWidth() - view.getMeasuredWidth();
	                } else {
	                    left = 0;
	                }
	            }
	            right = left + view.getMeasuredWidth();
	            bottom = top + view.getMeasuredHeight();
	            view.layout(left, top, right, bottom);
	            top = top + view.getMeasuredHeight();
	        }
	//        super.onLayout(changed, l, t, r, b);
	    }
	
	    public void changeItem() {
	        isLeft = !isLeft;
	        requestLayout();
	    }
	}
