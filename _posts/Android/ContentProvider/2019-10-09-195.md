---
layout: post
title:    查询联系人 
category: ContentProvider
tags: [ContentProvider]
excerpt:  查询联系人 
---




- 微信、QQ、陌陌... 
- 联系人相关的三张表 
	- data表:data1列,存的是联系人所有的信息(包括 电话 邮箱 姓名 地址)
	- raw_contacts表:contact_id列,表示应用一共有几条联系人 
	- mimetype表:id字段,用来区分联系人信息 
- 查询联系人的步骤 
	- 先查询raw_contacts的contact_id字段就知道一共有几条联系人 
	- 在查询data表:先查询data1字段和mimetype_id字段 
- Invalid column mimetype_id() :报mimetype_id列无效 1:列名写错了 2.表中没有这列。

-
    
    public static List<Contract> queryContract(Context context) {
        List<Contract> contracts = new ArrayList<>();
        Uri uri = Uri.parse("content://com.android.contacts/raw_contacts");
        Uri uri1 = Uri.parse("content://com.android.contacts/data");
        Cursor cursor = context.getContentResolver().query(uri, new String[]{"contact_id"}, null, null, null);
        Log.e(TAG, "queryContract: " + (cursor == null));
        if (cursor != null) {
            while (cursor.moveToNext()) {
                Contract contract = new Contract();
                String contactid = cursor.getString(0);
                Log.e(TAG, "queryContract: "+contactid );
                Cursor query = context.getContentResolver().query(uri1, new String[]{"data1", "mimetype"}, "raw_contact_id=?",
                        new String[]{contactid}, null);
                if (query != null) {
                    while (query.moveToNext()) {
                        String data1 = query.getString(0);
                        String mimetype = query.getString(1);
                        Log.e(TAG, "queryContract: "+data1+"===="+mimetype );
                        if (mimetype.equals("vnd.android.cursor.item/phone_v2")) {
                            contract.setPhone(data1);
                        } else if (mimetype.equals("vnd.android.cursor.item/name")) {
                            contract.setName(data1);
                        } else if (mimetype.equals("vnd.android.cursor.item/email_v2")) {
                            contract.setEmail(data1);
                        }
                    }
                }
                contracts.add(contract);
            }
        }
        return contracts;
    }
