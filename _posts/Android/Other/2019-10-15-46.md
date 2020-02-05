---
layout: post
title:    通知  
category: Other
tags: [Other]
excerpt:  通知 
---

给用户友好提示的方式: 1 Toast、2 对话框、3 通知

    public void click5(View view) {
        mNm = (NotificationManager) getSystemService(NOTIFICATION_SERVICE);
        Intent intent = new Intent(Intent.ACTION_DIAL);
        Uri uri = Uri.parse("tel:" + 10010);
        intent.setData(uri);
        PendingIntent pi = PendingIntent.getActivity(this, 7219, intent, PendingIntent.FLAG_ONE_SHOT);
        Notification build = null;
        if (android.os.Build.VERSION.SDK_INT >= android.os.Build.VERSION_CODES.JELLY_BEAN) {
            build = new Notification.Builder(this)
                    .setContentTitle("小青")
                    .setContentText("老地方见")
                    .setSmallIcon(R.mipmap.ic_launcher)
                    .setLargeIcon(BitmapFactory.decodeResource(getResources(), R.mipmap.ic_launcher))
                    .setContentIntent(pi)
                    .setDefaults(Notification.DEFAULT_ALL)
                    .build();
            mNm.notify(9127,build);
        }
    }

    public void click6(View view) {
        mNm.cancel(9127);
    }

 