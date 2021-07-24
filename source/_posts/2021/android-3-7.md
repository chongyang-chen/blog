---
title: android学习笔记（3-7）
categories:
  - android
tags:
  - android
date: 2021-02-28 11:42:58
---

android学习笔记。创建自定义控件。

<!-- more -->

新建TitleLayout继承自LinearLayout，代码如下：

```java
package com.example.uicustomview;

import android.app.Activity;
import android.content.Context;
import android.util.AttributeSet;
import android.view.LayoutInflater;
import android.widget.Button;
import android.widget.LinearLayout;
import android.widget.Toast;

import androidx.annotation.Nullable;

public class TitleLayout extends LinearLayout {

    public TitleLayout(Context context, @Nullable AttributeSet attrs) {
        super(context, attrs);
        LayoutInflater.from(context).inflate(R.layout.title, this);
        Button titleBack = (Button) findViewById(R.id.title_back);
        Button titleEdit = (Button) findViewById(R.id.title_edit);
        titleBack.setOnClickListener(v -> ((Activity)getContext()).finish());
        titleEdit.setOnClickListener(v -> Toast.makeText(getContext(),
                "You clicked Edit button.", Toast.LENGTH_SHORT).show());

    }
}
```



修改activity_main.xml，代码如下：

```xml
<com.example.uicustomview.TitleLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    tools:ignore="MissingConstraints" />
```



运行程序，点击返回按钮退出程序，点击编辑按钮，显示提示框。

<img src="01.png" width=480px>

接下来学习一个重要的控件——**ListView**。

