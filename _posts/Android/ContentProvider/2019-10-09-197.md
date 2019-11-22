---
layout: post
title:    短信备份
category: ContentProvider
tags: [ContentProvider]
excerpt:  短信备份
---

## 代码实现过程 ##

### 1、提供内容解析者把短信数据取出来 ###


    
    Uri uri = Uri.parse("content://sms/");
    Cursor cursor = getContentResolver().query(uri, new String[]{"address", "body", "date"}, null, null, null);


### 2、使用xml序列化把数据保存到xml文件中 ###

    
    private void backup() {
        try {
            XmlSerializer xmlSerializer = Xml.newSerializer();
            String path = getFilesDir().getAbsoluteFile() + File.separator + "sms.xml";
            Log.e(TAG, "backup: "+path );
            File file = new File(path);
            FileOutputStream fos = new FileOutputStream(file);
            xmlSerializer.setOutput(fos, "UTF-8");
            xmlSerializer.startDocument("UTF-8", true);
            xmlSerializer.startTag(null, "smss");
            Uri uri = Uri.parse("content://sms/");
            Cursor cursor = getContentResolver().query(uri, new String[]{"address", "body", "date"}, null, null, null);
            if (cursor != null) {
                while (cursor.moveToNext()) {
                    xmlSerializer.startTag(null, "sms");
                    xmlSerializer.startTag(null, "address");
                    String address = cursor.getString(0);
                    if (address == null || address.equals("") || address.equals("null")) {
                        xmlSerializer.text(" ");
                    } else {
                        xmlSerializer.text(address);
                    }
                    xmlSerializer.endTag(null, "address");
                    xmlSerializer.startTag(null, "body");
                    String body = cursor.getString(1);
                    if (body == null || body.equals("") || body.equals("null")) {
                        xmlSerializer.text(" ");
                    } else {
                        xmlSerializer.text(body);
                    }
                    xmlSerializer.endTag(null, "body");
                    xmlSerializer.startTag(null, "date");
                    String date = cursor.getString(2);
                    if (date == null || date.equals("") || date.equals("null")) {
                        xmlSerializer.text(" ");
                    } else {
                        xmlSerializer.text(date);
                    }
                    xmlSerializer.endTag(null, "date");

                    xmlSerializer.endTag(null, "sms");
                }
            }
            xmlSerializer.endTag(null, "smss");
            xmlSerializer.endDocument();
            Toast.makeText(this, "备份成功", Toast.LENGTH_SHORT).show();
        } catch (IOException e) {
            Toast.makeText(this, "备份失败", Toast.LENGTH_SHORT).show();
            e.printStackTrace();
        }
    }
            

