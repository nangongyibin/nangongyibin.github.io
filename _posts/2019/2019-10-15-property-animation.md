---
layout: post
title:    Android中动画----属性动画  
category: Other
tags: [Other]
excerpt:  Android中动画----属性动画 
---



	    public void click1(View view) {
	        Log.e(TAG, "click0: 平移");
	//        TranslateAnimation translateAnimation = new TranslateAnimation(TranslateAnimation.RELATIVE_TO_PARENT, 0.0f,
	//                TranslateAnimation.RELATIVE_TO_PARENT, 1.0f, TranslateAnimation.RELATIVE_TO_PARENT, 0.0f, TranslateAnimation.RELATIVE_TO_PARENT,
	//                1.0f);
	//        translateAnimation.setDuration(2000);
	//        translateAnimation.setRepeatCount(2);
	//        translateAnimation.setRepeatMode(Animation.REVERSE);
	//        mIv.startAnimation(translateAnimation);
	        ObjectAnimator oa = ObjectAnimator.ofFloat(mIv, "translationX", 0.0f, 10.0f, 20.0f, 30.0f);
	        oa.setDuration(2000);
	        oa.start();
	    }
	
	    public void click2(View view) {
	//        ScaleAnimation scaleAnimation = new ScaleAnimation(1.0f, 0.5f, 1.0f, 0.5f, ScaleAnimation.RELATIVE_TO_SELF, ScaleAnimation.RELATIVE_TO_SELF);
	//        scaleAnimation.setDuration(2000);
	//        scaleAnimation.setRepeatCount(2);
	//        scaleAnimation.setRepeatMode(Animation.REVERSE);
	//        mIv.startAnimation(scaleAnimation);
	        ObjectAnimator oa = ObjectAnimator.ofFloat(mIv, "scaleX", 1.0f, 2.0f);
	        oa.setDuration(2000);
	        oa.start();
	    }
	
	    public void click3(View view) {
	//        AlphaAnimation alphaAnimation = new AlphaAnimation(1.0f, 0.0f);
	//        alphaAnimation.setDuration(2000);
	//        alphaAnimation.setRepeatCount(2);
	//        alphaAnimation.setRepeatMode(Animation.REVERSE);
	//        mIv.startAnimation(alphaAnimation);
	        ObjectAnimator oa = ObjectAnimator.ofFloat(mIv, "alpha", 0.0f, 1.0f);
	        oa.setDuration(2000);
	        oa.start();
	    }
	
	    public void click4(View view) {
	//        AnimationSet animationSet = new AnimationSet(true);
	////        RotateAnimation rotateAnimation = new RotateAnimation(0, 360, RotateAnimation.RELATIVE_TO_SELF,
	////                RotateAnimation.RELATIVE_TO_SELF);
	////        TranslateAnimation translateAnimation = new TranslateAnimation(TranslateAnimation.RELATIVE_TO_PARENT, 0.0f,
	////                TranslateAnimation.RELATIVE_TO_PARENT, 1.0f, TranslateAnimation.RELATIVE_TO_PARENT, 0.0f, TranslateAnimation.RELATIVE_TO_PARENT,
	////                1.0f);
	////        ScaleAnimation scaleAnimation = new ScaleAnimation(1.0f, 0.5f, 1.0f, 0.5f, ScaleAnimation.RELATIVE_TO_SELF, ScaleAnimation
	// .RELATIVE_TO_SELF);
	////        AlphaAnimation alphaAnimation = new AlphaAnimation(1.0f, 0.0f);
	////        animationSet.addAnimation(rotateAnimation);
	////        animationSet.addAnimation(translateAnimation);
	////        animationSet.addAnimation(scaleAnimation);
	////        animationSet.addAnimation(alphaAnimation);
	////        animationSet.setDuration(2000);
	////        animationSet.setRepeatCount(2);
	////        animationSet.setRepeatMode(Animation.REVERSE);
	////        mIv.startAnimation(animationSet);
	        ObjectAnimator oa = ObjectAnimator.ofFloat(mIv, "rotation", 0.0f, 90.0f, 180.0f, 270.0f, 360.0f);
	        ObjectAnimator oa1 = ObjectAnimator.ofFloat(mIv, "alpha", 0.0f, 1.0f);
	        ObjectAnimator oa2 = ObjectAnimator.ofFloat(mIv, "scaleX", 1.0f, 2.0f);
	        ObjectAnimator oa3 = ObjectAnimator.ofFloat(mIv, "translationX", 0.0f, 10.0f, 20.0f, 30.0f);
	        AnimatorSet set = new AnimatorSet();
	        set.playSequentially(oa,oa1,oa2,oa3);
	        set.setDuration(2000);
	        set.setTarget(mIv);
	        set.start();
	    }
	
	    public void click0(View view) {
	        Log.e(TAG, "click0: 旋转");
	//        RotateAnimation rotateAnimation = new RotateAnimation(0, 360, RotateAnimation.RELATIVE_TO_SELF,
	//                RotateAnimation.RELATIVE_TO_SELF);
	//        rotateAnimation.setDuration(2000);
	//        rotateAnimation.setRepeatCount(2);
	//        rotateAnimation.setRepeatMode(Animation.REVERSE);
	//        mIv.startAnimation(rotateAnimation);
	        ObjectAnimator oa = ObjectAnimator.ofFloat(mIv, "rotation", 0.0f, 90.0f, 180.0f, 270.0f, 360.0f);
	        oa.setDuration(2000);
	        oa.start();
	    }

属性动画：会改变控件真实的坐标。