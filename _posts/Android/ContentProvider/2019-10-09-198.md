---
layout: post
title:    生成虚拟短信(API19以下)
category: ContentProvider
tags: [ContentProvider]
excerpt:  生成虚拟短信(API19以下)
---


    public void make(View view) {
        try {
            Uri uri = Uri.parse("content://sms/");
            ContentValues values = new ContentValues();
            values.put("address", "18534867219");
            values.put("body", "天道酬勤，追梦无疆");
            values.put("type", "1");
            values.put("date", System.currentTimeMillis());
            Uri insert = getContentResolver().insert(uri, values);
            Log.e(TAG, "make: " + insert.toString());
        } catch (Exception e) {
            Log.e(TAG, "make: " + e.getLocalizedMessage());
            e.printStackTrace();
        }
    }
