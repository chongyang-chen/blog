---
title: android学习笔记（2）
categories:
  - android
tags:
  - android
date: 2021-02-23 21:05:51
---

今天来学习第二章的内容，探究活动，也就是Activity。

<!-- more -->

为了学习本章的内容需要新建一个No Activity的项目。

<img src="01.png" width=600px>

新建一个 Activity，编辑xml文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">
    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Button One"
        android:id="@+id/button_1"
        ></Button>
</LinearLayout>
```

修改FirstActivity.java:

```java
setContentView(R.layout.first_layout);
```

最后修改Manifest.xml

```xml
<activity
    android:name=".FirstActivity"
    android:label="FirstActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

上面代码手动创建了一个活动。

### 如何在活动中使用Toast和Menu。

```java
    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.main, menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(@NonNull MenuItem item) {
        switch (item.getItemId()){
            case R.id.add_item:
                Toast.makeText(this, "You clicked Add.", Toast.LENGTH_SHORT).show();
                break;
            case R.id.remove_item:
                Toast.makeText(this, "You clicked Remove.", Toast.LENGTH_SHORT).show();
                break;
            case R.id.delete_item:
                finish();
                break;
            default:
        }
        return true;
    }
```



menu.xml:

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@+id/add_item" android:title="Add">

    </item>
    <item android:id="@+id/remove_item" android:title="Remove">

    </item>
    <item android:id="@+id/delete_item" android:title="Delete">

    </item>
</menu>
```

### 使用Intent在活动间穿梭

使用显式Intent和使用隐式Intent两种方法。

使用Intent还可以打开浏览器以及系统拨号界面。

向下一个活动传递数据以及返回数据给上一个活动。

### 活动的生命周期

四种状态：运行，暂停，停止，销毁。

7个回调方法：

```java
onCreate()
onStart()
onResume()
onPause()
onStop()
onDestory()
onRestart()
```

下面是一张生命周期的示意图：

<img src="02.png" width=480px>

Activity中有个一方法onSaveInstanceState()在活动被回收之前调用，可以在这个方法中保存临时数据。

### 活动的启动模式

启动模式有4种：standard，singleTop，singleTask，singleInstance。

其中最后一种模式是最复杂的一个。

最后是关于活动的最佳实践。

知晓当前是哪一个活动，随时退出程序，启动活动的最佳写法。

### 小结

本章的内容较多，用了两天的时间才学完本章，本章的大部分代码都能成功的运行，也有部分代码显示错误，总体上还可以。没有打消自己学习android的积极性。再接再厉，开始下一张的学习。

