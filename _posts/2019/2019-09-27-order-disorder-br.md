---
layout: post
title: 自定义广播
category: BroadcastReceiver
tags: [BroadcastReceiver]
excerpt: 自定义广播
---

### 有序广播: ###


特点:类似中央发送红头文件.

    
    public void disorder(View view) {
        Intent intent = new Intent(this, MyOrderReceiver.class);
        intent.setAction("com.ngyb.disorder");
        intent.putExtra("name", "我爱成青青一生一世");
        sendBroadcast(intent);
    }

### 无序广播: ###

 
 特点:类似新闻联播,每天晚上7点准时开播.
   
        
    public void order(View view) {
        Intent intent = new Intent();
        intent.setAction("com.ngyb.order.rice");
	//        sendOrderedBroadcast(intent,null);
        sendOrderedBroadcast(intent,null,new Final(),null,1,"习大大发放了100斤大米",null);
    }



总结:有序广播可以被终止,数据可以被修改,无序广播不可以被终止,数据不可以修改.






