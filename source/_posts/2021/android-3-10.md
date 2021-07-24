---
title: android学习笔记（3-10）
categories:
  - android
tags:
  - android
  - 聊天界面
date: 2021-02-28 15:17:00
---

android学习笔记。最佳实践——聊天界面。

<!-- more -->

新建一个项目UIBestPractice：

<img src="01.png" width=800px>

Nine-Patch 图片。

编写聊天界面。

activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#d8e0e0"
    android:orientation="vertical">

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/msg_recycler_view"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <EditText
            android:id="@+id/input_text"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:hint="Type something here."
            android:maxLines="2" />

        <Button
            android:id="@+id/send"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="send" />

    </LinearLayout>


</LinearLayout>
```

msg_item.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:padding="10dp">

    <LinearLayout
        android:id="@+id/left_layout"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="start"
        android:background="@drawable/message_left">

        <TextView
            android:id="@+id/left_msg"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:layout_margin="10dp"
            android:textColor="#fff"/>
    </LinearLayout>

    <LinearLayout
        android:id="@+id/right_layout"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="end"
        android:background="@drawable/message_right">

        <TextView
            android:id="@+id/right_msg"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:layout_margin="10dp" />
    </LinearLayout>

</LinearLayout>
```



MsgAdapter.java

```java
package com.example.uibestpractice;

import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.LinearLayout;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.recyclerview.widget.RecyclerView;

import java.util.List;

public class MsgAdapter extends RecyclerView.Adapter<MsgAdapter.ViewHolder> {
    private final List<Msg> mMsgList;
    public static class ViewHolder extends RecyclerView.ViewHolder {
        LinearLayout leftLayout;
        LinearLayout rightLayout;
        TextView leftMsg;
        TextView rightMsg;

        public ViewHolder(View view){
            super(view);
            leftLayout = (LinearLayout)view.findViewById(R.id.left_layout);
            rightLayout = (LinearLayout)view.findViewById(R.id.right_layout);
            leftMsg = (TextView) view.findViewById(R.id.left_msg);
            rightMsg = (TextView)view.findViewById(R.id.right_msg);
        }

    }
    public MsgAdapter(List<Msg> msgList){
        mMsgList = msgList;
    }

    @NonNull
    @Override
    public ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).
                inflate(R.layout.msg_item,parent,false);
        return new ViewHolder(view);
    }

    @Override
    public void onBindViewHolder(@NonNull ViewHolder holder, int position) {
        Msg msg = mMsgList.get(position);
        if (msg.getType() == Msg.TYPE_RECEIVED){
            holder.leftLayout.setVisibility(View.VISIBLE);
            holder.rightLayout.setVisibility(View.GONE);
            holder.leftMsg.setText(msg.getContent());
        } else if (msg.getType() == Msg.TYPE_SEND){
            holder.leftLayout.setVisibility(View.GONE);
            holder.rightLayout.setVisibility(View.VISIBLE);
            holder.rightMsg.setText(msg.getContent());

        }
    }

    @Override
    public int getItemCount() {
        return mMsgList.size();
    }
}
```



MainActivity.java

```java
package com.example.uibestpractice;

import androidx.appcompat.app.AppCompatActivity;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;

import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;

import java.util.ArrayList;
import java.util.List;

public class MainActivity extends AppCompatActivity {

    private final List<Msg> msgList = new ArrayList<>();
    private EditText inputText;
    private RecyclerView msgRecyclerView;
    private MsgAdapter adapter;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        initMsg();
        inputText = (EditText)findViewById(R.id.input_text);
        Button send = (Button) findViewById(R.id.send);
        msgRecyclerView = (RecyclerView)findViewById(R.id.msg_recycler_view);
        LinearLayoutManager layoutManager = new LinearLayoutManager(this);
        msgRecyclerView.setLayoutManager(layoutManager);
        adapter = new MsgAdapter(msgList);
        msgRecyclerView.setAdapter(adapter);
        send.setOnClickListener(v -> {
            String content = inputText.getText().toString();
            if (!"".equals(content)){
                Msg msg = new Msg(content, Msg.TYPE_SEND);
                msgList.add(msg);
                adapter.notifyItemInserted(msgList.size() - 1);
                Msg msg2 = new Msg(content, Msg.TYPE_RECEIVED);
                msgList.add(msg2);
                adapter.notifyItemInserted(msgList.size() - 1);
                msgRecyclerView.scrollToPosition(msgList.size() - 1);
                inputText.setText("");
            }
        });
    }
    private void initMsg(){
        Msg msg1 = new Msg("你是谁？", Msg.TYPE_SEND);
        msgList.add(msg1);
        Msg msg2 = new Msg("你是谁？", Msg.TYPE_RECEIVED);
        msgList.add(msg2);
        Msg msg3 = new Msg("我是你爸爸。", Msg.TYPE_SEND);
        msgList.add(msg3);
        Msg msg4 = new Msg("我是你爸爸。", Msg.TYPE_RECEIVED);
        msgList.add(msg4);
    }
}
```



Msg.java

```java
package com.example.uibestpractice;

import androidx.appcompat.app.AppCompatActivity;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;

import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;

import java.util.ArrayList;
import java.util.List;

public class MainActivity extends AppCompatActivity {

    private final List<Msg> msgList = new ArrayList<>();
    private EditText inputText;
    private RecyclerView msgRecyclerView;
    private MsgAdapter adapter;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        initMsg();
        inputText = (EditText)findViewById(R.id.input_text);
        Button send = (Button) findViewById(R.id.send);
        msgRecyclerView = (RecyclerView)findViewById(R.id.msg_recycler_view);
        LinearLayoutManager layoutManager = new LinearLayoutManager(this);
        msgRecyclerView.setLayoutManager(layoutManager);
        adapter = new MsgAdapter(msgList);
        msgRecyclerView.setAdapter(adapter);
        send.setOnClickListener(v -> {
            String content = inputText.getText().toString();
            if (!"".equals(content)){
                Msg msg = new Msg(content, Msg.TYPE_SEND);
                msgList.add(msg);
                adapter.notifyItemInserted(msgList.size() - 1);
                Msg msg2 = new Msg(content, Msg.TYPE_RECEIVED);
                msgList.add(msg2);
                adapter.notifyItemInserted(msgList.size() - 1);
                msgRecyclerView.scrollToPosition(msgList.size() - 1);
                inputText.setText("");
            }
        });
    }
    private void initMsg(){
        Msg msg1 = new Msg("你是谁？", Msg.TYPE_SEND);
        msgList.add(msg1);
        Msg msg2 = new Msg("你是谁？", Msg.TYPE_RECEIVED);
        msgList.add(msg2);
        Msg msg3 = new Msg("我是你爸爸。", Msg.TYPE_SEND);
        msgList.add(msg3);
        Msg msg4 = new Msg("我是你爸爸。", Msg.TYPE_RECEIVED);
        msgList.add(msg4);
    }
}
```

运行结果如下：

<img src="02.png" width=480px>

这是学完本章，完成的第一个功能界面。

通过本章的学习对Android控件有了一定的了解，掌握xml来编辑布局，并设置相关的属性。需要更多的练习才能熟练掌握这些知识。

加油吧，打工人。

