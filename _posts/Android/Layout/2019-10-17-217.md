---
layout: post
title:    view绘制流程  
category: Layout
tags: [Layout]
excerpt:  view绘制流程
---

[1]测量 

measure方法完成对view测量 –>实际测量工作在onMeasure方法里面实现，因为measure方法是final的 –>最终调用setMeasuredDimension这个方法完成测量工作，当我们想自己对view进行测量的时候，重写onMeasure方法，调用setMeasuredDimension方法就可以了。

[2]排版 

底层调用layout —->setFrame方法完成对view摆放。
 
view在屏幕占据的是一个矩形区域，view的职责是绘制和事件处理。

[3]绘制 draw

    *      1. Draw the background   画背景

    *      2. If necessary, save the canvas' layers to prepare for fading  画图层 跳过

    *      3. Draw view's content   画内容 -->重写onDraw

    *      4. Draw children   画孩子  当继承ViewGropp的时候才涉及画孩子

    *      5. If necessary, draw the fading edges and restore layers  跳过

    *      6. Draw decorations (scrollbars for instance)  画滚动条


[4]绘制实战 

4.1)画线

	canvas.drawLine(77f, 99f, 721f, 912f, paint);

4.2) 画圆

	canvas.drawCircle(100f,100f,79f,paint);

4.3)画图片

	Bitmap bitmap = BitmapFactory.decodeResource(getResources(), R.drawable.haha);
	canvas.drawBitmap(bitmap,new Matrix(),paint);

4.3)画三角形，三个点连接起来

        Path path = new Path();
        path.lineTo(10f, 10f);
        path.lineTo(10f, 721f);
        path.lineTo(721f, 10f);
        canvas.drawPath(path, paint);

4.4)画弧 

        RectF rectF = new RectF(0f, 0f, 195f, 195f);
        canvas.drawArc(rectF, 0, pg, false, paint);