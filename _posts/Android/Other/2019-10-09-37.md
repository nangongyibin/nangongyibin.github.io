---
layout: post
title:    加载大图片 
category: Other
tags: [Other]
excerpt:  加载大图片 
---

## 当加载大图片的时候 报如下错误Caused by: java.lang.OutOfMemoryError (内存溢出) ##

## 代码实现过程  ##

### 1、获取手机分辨率 ###


        WindowManager wm = (WindowManager) getSystemService(Service.WINDOW_SERVICE);
        Display defaultDisplay = wm.getDefaultDisplay();
        Point point = new Point();
        defaultDisplay.getSize(point);
        mWidth = point.x;
        mHeight = point.y;

	
### 2、获取图片的宽和高 ###

        BitmapFactory.Options options = new BitmapFactory.Options();
        options.inJustDecodeBounds = true;
        BitmapFactory.decodeResource(getResources(), R.mipmap.big, options);
        int outWidth = options.outWidth;
        int outHeight = options.outHeight;


### 3、计算缩放比:  ###

假设图片 2400 ＊3200 

320 480 7 6 按照大的缩放

        
		int scaleY = outHeight / mHeight;
        int scaleX = outWidth / mWidth;
        int scale;
        if (scaleX > scaleY) {
            scale = scaleX;
        } else {
            scale = scaleY;
        }

### 4、按照缩放比加载图片 ###

        options.inJustDecodeBounds = false;
        options.inSampleSize = scale;
        Bitmap bitmap = BitmapFactory.decodeResource(getResources(), R.mipmap.big, options);
        mIv.setImageBitmap(bitmap);