---
layout: post
title:    创建原图的副本
category: Other
tags: [Other]
excerpt:  创建原图的副本
---


    private void copyBitmap() {
        Bitmap bitmap = BitmapFactory.decodeResource(getResources(), R.mipmap.tomcat);
        mIv.setImageBitmap(bitmap);
        Bitmap bitmapC = Bitmap.createBitmap(bitmap.getWidth(), bitmap.getHeight(), bitmap.getConfig());
        Paint paint = new Paint();
        Canvas canvas = new Canvas(bitmapC);
        Matrix matrix = new Matrix();
        matrix.setScale(1.0f,-1.0f);
        matrix.postTranslate(0,bitmap.getHeight());
        canvas.drawBitmap(bitmap, matrix, paint);
        mIvC.setImageBitmap(bitmapC);

    }


通过matrix实现图形特殊效果 

- 旋转 
- 缩放 
- 移动 
- 镜面 
- 倒影


-

        Matrix matrix = new Matrix();
        matrix.setScale(1.0f,-1.0f);
        matrix.postTranslate(0,bitmap.getHeight());


    
