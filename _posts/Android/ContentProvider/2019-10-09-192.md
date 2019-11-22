---
layout: post
title:    通过内容提供者向联系人数据库插入联系人
category: ContentProvider
tags: [ContentProvider]
excerpt:  通过内容提供者向联系人数据库插入联系人 
---


 
- 插入联系人的步骤
	- 先往raw_contacts 表插入数据，更新contact_id
	- 在往data表里面插入数据

-
    
    
    public void insertContract(View view) {
        String name = mEt.getText().toString().trim();
        String phone = mEt1.getText().toString().trim();
        String email = mEt2.getText().toString().trim();
        Uri uri = Uri.parse("content://com.android.contacts/raw_contacts");
        Uri uri1 = Uri.parse("content://com.android.contacts/data");
        Cursor cursor = getContentResolver().query(uri, new String[]{"contact_id"}, null, null, null);
        int count = cursor.getCount()+1;
        ContentValues value0 = new ContentValues();
        value0.put("contact_id",count);
        getContentResolver().insert(uri, value0);
        ContentValues value1 = new ContentValues();
        value1.put("raw_contact_id",count);
        value1.put("data1",name);
        value1.put("mimetype","vnd.android.cursor.item/name");
        getContentResolver().insert(uri1,value1);
        ContentValues value2 = new ContentValues();
        value2.put("raw_contact_id",count);
        value2.put("data1",phone);
        value2.put("mimetype","vnd.android.cursor.item/phone_v2");
        getContentResolver().insert(uri1,value2);
        ContentValues value3 = new ContentValues();
        value3.put("raw_contact_id",count);
        value3.put("data1",email);
        value3.put("mimetype","vnd.android.cursor.item/email_v2");
        getContentResolver().insert(uri1,value3);
    }