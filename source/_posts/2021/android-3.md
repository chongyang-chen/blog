---
title: android学习笔记（3）
categories:
  - android
tags:
  - android
date: 2021-02-24 21:13:50
---

今天开始学习UI开发，上一章学习的Button就属于UI，下面来学习更过的UI知识。

<!-- more -->

新建一个项目：

<img src="01.png" width=600px>

### TextView

修改activity_main.xml代码：

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/text_view"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="This is a TextView!" />
</LinearLayout>
```

运行程序显示结果如下图所示：

<img src="02.png" width=480px>

接下来设置对齐方式：

```xml
<TextView
        android:id="@+id/text_view"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:text="This is a TextView!" />
```



不出所料，文字居中显示。

<img src="03.png" width=480px>

另外还可以设置文字的字体大小和颜色，是不是很简单。

<img src="04.png" width=480px>