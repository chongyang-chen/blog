---
title: android学习笔记（3-4）
categories:
  - android
tags:
  - android
date: 2021-02-27 12:26:20
---

android学习笔记。今天学习layout_weight属性的知识。

<!-- more -->

使用下面的代码：

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">

    <EditText
        android:id="@+id/input_message"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:hint="请输入用户名" />

    <Button
        android:id="@+id/login"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:text="登录" />
</LinearLayout>
```

结果如下，两个控件在水平方向各占一半。

dp是Android中指定控件大小，间距等属性的单位，layout_width 指定0dp是一种规范的写法。可以指定部分控件的layout_weight 属性来实现更好的布局效果。

<img src="01.png" width=480px>

### 相对布局

在屏幕四角和中心，分别放置按钮。

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:id="@+id/button_1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentLeft="true"
        android:layout_alignParentTop="true"
        android:text="Button 1"></Button>

    <Button
        android:id="@+id/button_2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentRight="true"
        android:layout_alignParentTop="true"
        android:text="Button 2"></Button>

    <Button
        android:id="@+id/button_3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="Button 3"></Button>

    <Button
        android:id="@+id/button_4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentLeft="true"
        android:layout_alignParentBottom="true"
        android:text="Button 4"></Button>

    <Button
        android:id="@+id/button_5"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentRight="true"
        android:layout_alignParentBottom="true"
        android:text="Button 5"></Button>
</RelativeLayout>
```



效果如下：

<img src="02.png" width=480px>



修改代码，以中心按钮作为参照。

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:id="@+id/button_3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="Button 3" />

    <Button
        android:id="@+id/button_1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_above="@+id/button_3"
        android:layout_toStartOf="@id/button_3"
        android:text="Button 1" />

    <Button
        android:id="@+id/button_2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_above="@id/button_3"
        android:layout_toEndOf="@id/button_3"
        android:text="Button 2" />
    
    <Button
        android:id="@+id/button_4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/button_3"
        android:layout_toStartOf="@id/button_3"
        android:text="Button 4" />

    <Button
        android:id="@+id/button_5"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/button_3"
        android:layout_toEndOf="@id/button_3"
        android:text="Button 5" />
</RelativeLayout>
```



效果如下：

<img src="03.png" width=480px>