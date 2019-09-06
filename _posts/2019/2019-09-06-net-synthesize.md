---
layout: post
title: 网络编程综合案例
category: NetLib
tags: [NetLib]
excerpt: 网络编程综合案例
---


## 案例设计到知识点：listview —>baseAdapter，tomcat xml(xml解析) url httpurlconnection 开线程 handler  ##

## 案例开发的流程  ##

### 开发这样一个程序，最少3个人，一个android客户端,一个UI设计师,做服务器开发人员。产品经理(微信)  ###

## 代码实现过程:  ##

### 画UI ###

    <?xml version="1.0" encoding="utf-8"?>
	<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:layout_width="match_parent"
	    android:layout_height="100dp">
	
	    <com.loopj.android.image.SmartImageView
	        android:id="@+id/siv"
	        android:layout_width="100dp"
	        android:layout_height="100dp"
	        android:src="@mipmap/ic_launcher" />
	
	    <LinearLayout
	        android:layout_width="match_parent"
	        android:layout_height="match_parent"
	        android:layout_toRightOf="@id/siv"
	        android:orientation="vertical">
	
	        <TextView
	            android:id="@+id/tv1"
	            android:layout_width="match_parent"
	            android:layout_height="0dp"
	            android:layout_weight="1"/>
	
	        <TextView
	            android:id="@+id/tv2"
	            android:layout_width="match_parent"
	            android:layout_height="0dp"
	            android:layout_weight="1" />
	    </LinearLayout>
	</RelativeLayout>


### 搭建服务器，去服务器取数据 ###

    
    private void initData() {
        try {
            URL url = new URL("http://it.nangongyibin.com:8080/resource/news.xml");
            HttpsURLConnection conn = (HttpsURLConnection) url.openConnection();
            int code = conn.getResponseCode();
            if (code == 200) {
                InputStream is = conn.getInputStream();
                mNews = NewsXmlUtils.parseXml(is);
                if (myadapter ==null){
                    myadapter = new MyAdapter();
                    mLv.setAdapter(myadapter);
                }else{
                    myadapter.notifyDataSetChanged();
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

   
### 对数据进行解析 xml解析 ###
 
    
    public static List<News> parseXml(InputStream is) {
        List<News> list = null;
        News news = null;
        try {
            XmlPullParser parser = Xml.newPullParser();
            parser.setInput(is, "UTF-8");
            int eventType = parser.getEventType();
            while (eventType != XmlPullParser.END_DOCUMENT) {
                switch (eventType) {
                    case XmlPullParser.START_TAG:
                        if ("channel".equals(parser.getName())) {
                            list = new ArrayList<>();
                        } else if ("item".equals(parser.getName())) {
                            news = new News();
                        } else if ("title".equals(parser.getName())) {
                            news.setTitle(parser.nextText());
                        } else if ("description".equals(parser.getName())) {
                            news.setDescription(parser.nextText());
                        } else if ("image".equals(parser.getName())) {
                            news.setImage(parser.nextText());
                        } else if ("type".equals(parser.getName())) {
                            news.setType(parser.nextText());
                        } else if ("comment".equals(parser.getName())) {
                            news.setComment(parser.nextText());
                        }
                        break;
                    case XmlPullParser.END_TAG:
                        if ("item".equals(parser.getName())) {
                            list.add(news);
                        }
                        break;
                }
                eventType = parser.next();
            }
            return list;
        } catch (XmlPullParserException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;
    }


### 定义数据适配器 ###

    
    public class MyAdapter extends BaseAdapter {

        @Override
        public int getCount() {
            if (mNews != null) {
                return mNews.size();
            }
            return 0;
        }

        @Override
        public Object getItem(int position) {
            return null;
        }

        @Override
        public long getItemId(int position) {
            return 0;
        }

        @Override
        public View getView(int position, View convertView, ViewGroup parent) {
            if (convertView == null) {
                convertView = View.inflate(MainActivity.this, R.layout.item, null);
            }
            SmartImageView siv = convertView.findViewById(R.id.siv);
            TextView tv1 = convertView.findViewById(R.id.tv1);
            TextView tv2 = convertView.findViewById(R.id.tv2);
            News news = mNews.get(position);
            siv.setImageUrl(news.getImage());
            tv1.setText(news.getTitle());
            tv2.setText(news.getDescription());
            return convertView;
        }
    }

## smartImageview  ##

### 要先声明 要求这个类的完整包名和类名 ###

    
    <com.loopj.android.image.SmartImageView
        android:id="@+id/siv"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:src="@mipmap/ic_launcher" />

### 找的控件 展示数据 ###

            SmartImageView siv = convertView.findViewById(R.id.siv);
            siv.setImageUrl(news.getImage());