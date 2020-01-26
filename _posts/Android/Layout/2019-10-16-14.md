---
layout: post
title:    下拉列表的实现（二）  
category: Layout
tags: [Layout]
excerpt:  下拉列表的实现（二） 
---

## 需求分析：通过edittext、button、popupwindow、listview组合达到自定义需求  ##


## 代码实现步骤 ##

### [1]画UI ###

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <EditText
            android:id="@+id/etNumber"
            android:layout_width="250dp"
            android:layout_height="wrap_content" />

        <ImageButton
            android:id="@+id/ib"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignEnd="@id/etNumber"
            android:layout_alignRight="@id/etNumber"
            android:background="@drawable/down_arrow"
            android:src="@null" />
    </RelativeLayout>

### [2]初始化popupwindow ###

    private void showPopupWindow() {
        ListView lv = initListView();
        final PopupWindow popupWindow = new PopupWindow(lv, mEtNumber.getWidth(), 1080, true);
        popupWindow.showAsDropDown(mEtNumber, 0, -20);
        lv.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                Log.e(TAG, "onItemClick: "+position );
                String str = list.get(position);
                mEtNumber.setText(str);
                popupWindow.dismiss();
            }
        });
    }


### [3]准备popupwindow要展示的内容—>listview 先画listview条目的布局 ###

	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:layout_width="match_parent"
	    android:layout_height="wrap_content"
	    android:descendantFocusability="blocksDescendants"
	    android:orientation="horizontal">
	
	    <ImageView
	        android:id="@+id/iv"
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content"
	        android:background="@drawable/user" />
	
	    <TextView
	        android:id="@+id/tv"
	        android:layout_width="0dp"
	        android:layout_height="wrap_content"
	        android:layout_gravity="center"
	        android:layout_weight="1"
	        android:gravity="center"
	        android:text="1008611"
	        android:textColor="@android:color/black" />
	
	    <ImageButton
	        android:id="@+id/ib"
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content"
	        android:layout_gravity="center"
	        android:background="@drawable/delete" />
	</LinearLayout>

### [4]展示listviet的数据 ###

    private ListView initListView() {
        ListView lv = (ListView) View.inflate(this, R.layout.listviewbg, null);
        lv.setDivider(new ColorDrawable(Color.GRAY));
        lv.setDividerHeight(1);
        MyAdapter myAdapter = new MyAdapter();
        lv.setAdapter(myAdapter);
        return lv;
    }


    class MyAdapter extends BaseAdapter {

        @Override
        public int getCount() {
            if (list != null && list.size() > 0) {
                return list.size();
            }
            return 0;
        }

        @Override
        public String getItem(int position) {
            return list.get(position);
        }

        @Override
        public long getItemId(int position) {
            return position;
        }

        @Override
        public View getView(final int position, View convertView, ViewGroup parent) {
            if (convertView == null) {
                convertView = View.inflate(getApplicationContext(), R.layout.item, null);
            }
            TextView tv = convertView.findViewById(R.id.tv);
            ImageView iv = convertView.findViewById(R.id.iv);
            ImageButton ib = convertView.findViewById(R.id.ib);
            ib.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    list.remove(getItem(position));
                    notifyDataSetChanged();
                }
            });
            tv.setText(getItem(position));
            return convertView;
        }
    }

### [5]点击listview的条目，把点击条目的数据取出来展示到edittext上 ###

        lv.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                Log.e(TAG, "onItemClick: "+position );
                String str = list.get(position);
                mEtNumber.setText(str);
                popupWindow.dismiss();
            }
        });


注意:当listview 的条目上有button、checkbox这些控件，会抢占条目的事件 —->解决方案在条目的根布局上面加如下属性

    android:descendantFocusability="blocksDescendants"

### [6]点击删除按钮逻辑  ###

            ib.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    list.remove(getItem(position));
                    notifyDataSetChanged();
                }
            });
