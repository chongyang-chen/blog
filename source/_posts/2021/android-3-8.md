---
title: android学习笔记（3-8）
categories:
  - android
tags:
  - android
  - ListView
date: 2021-02-28 11:43:01
---

android学习笔记。今天开始ListView的学习。

<!-- more -->

新建项目ListViewTest：

<img src="01.png" width=800px>

代码如下：

```xml
<ListView
    android:id="@+id/list_view"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintLeft_toLeftOf="parent"
    app:layout_constraintRight_toRightOf="parent"
    app:layout_constraintTop_toTopOf="parent" />
```

修改MainActivity.java:

```java
public class MainActivity extends AppCompatActivity {

    private String[] data = {
            "Test 1","Test 2","Test 3","Test 4","Test 5","Test 6",
            "Test 7","Test 8","Test 9","Test 10","Test 11","Test 12",
            "Test 13","Test 14","Test 15","Test 16","Test 17","Test 18",
            "Test 19","Test 20","Test 21","Test 22","Test 23","Test 24"
    };
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(this,
                android.R.layout.simple_list_item_1,data);
        ListView listView = (ListView)findViewById(R.id.list_view);
        listView.setAdapter(adapter);
    }
}
```

运行程序显示ListView：

<img src="02.png" width=480px>

首先准备一个数组，数组中的内容无法直接在ListView中显示，需要使用适配器来完成。simple_list_item_1 是Android内置的布局文件，用于简单的显示一段文本。

### 自定义ListView界面

新建一个Fruit类：

```java
package com.example.listviewtest;

public class Fruit {
    private String name;
    private int imageId;

    public Fruit(String name, int imageId) {
        this.name = name;
        this.imageId = imageId;
    }

    public int getImageId() {
        return imageId;
    }

    public String getName() {
        return name;
    }
}
```

在layout目录下新建fruit_item.xml。

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:ignore="UseCompoundDrawables">

    <ImageView
        android:id="@+id/fruit_image"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />

    <TextView
        android:id="@+id/fruit_name"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_vertical"
        android:layout_marginStart="10dp" />

</LinearLayout>
```

新建FruitAdapter类：

```java
package com.example.listviewtest;

import android.annotation.SuppressLint;
import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ArrayAdapter;
import android.widget.ImageView;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.annotation.Nullable;

import java.util.List;

public class FruitAdapter extends ArrayAdapter<Fruit> {

    private final int resourceId;

    public FruitAdapter(@NonNull Context context, int resource, @NonNull List<Fruit> objects) {
        super(context, resource, objects);
        resourceId = resource;
    }

    @NonNull
    @Override
    public View getView(int position, @Nullable View convertView, @NonNull ViewGroup parent) {
        Fruit fruit = getItem(position);
        @SuppressLint("ViewHolder") View view = LayoutInflater.from(getContext()).inflate(resourceId, parent, false);
        ImageView fruitImage = (ImageView) view.findViewById(R.id.fruit_image);
        TextView fruitName = (TextView) view.findViewById(R.id.fruit_name);
        fruitImage.setImageResource(fruit.getImageId());
        fruitName.setText(fruit.getName());
        return view;
    }
}
```

修改MainActivity.java:

```java
public class MainActivity extends AppCompatActivity {

    private List<Fruit> fruitList = new ArrayList<>();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        initFruits();
        FruitAdapter adapter = new FruitAdapter(this, R.layout.fruit_item,fruitList);
        ListView listView = (ListView)findViewById(R.id.list_view);
        listView.setAdapter(adapter);
    }
    private void initFruits(){
        for (int i = 0; i < 20; i++){
            Fruit apple = new Fruit("Apple", R.drawable.apple_pic);
            fruitList.add(apple);
        }
    }
}
```

结果如下图所示：

<img src="03.png" width=480px>

### 提升ListView

```java
@Override
public View getView(int position, @Nullable View convertView, @NonNull ViewGroup parent) {
    Fruit fruit = getItem(position);
    View view;
    if (convertView == null) {
        view = LayoutInflater.from(getContext()).inflate(resourceId, parent, false);
    } else {
        view = convertView;
    }
    ImageView fruitImage = (ImageView) view.findViewById(R.id.fruit_image);
    TextView fruitName = (TextView) view.findViewById(R.id.fruit_name);
    fruitImage.setImageResource(fruit.getImageId());
    fruitName.setText(fruit.getName());
    return view;
}
```

对 contentView 进行重用。

使用ViewHolder进行进一步优化。

```java
public class FruitAdapter extends ArrayAdapter<Fruit> {

    private final int resourceId;

    public FruitAdapter(@NonNull Context context, int resource, @NonNull List<Fruit> objects) {
        super(context, resource, objects);
        resourceId = resource;
    }

    @NonNull
    @Override
    public View getView(int position, @Nullable View convertView, @NonNull ViewGroup parent) {
        Fruit fruit = getItem(position);
        View view;
        ViewHolder viewHolder;
        if (convertView == null) {
            view = LayoutInflater.from(getContext()).inflate(resourceId, parent, false);
            viewHolder = new ViewHolder();
            viewHolder.fruitImage = (ImageView) view.findViewById(R.id.fruit_image);
            viewHolder.fruitName = (TextView) view.findViewById(R.id.fruit_name);
            view.setTag(viewHolder);
        } else {
            view = convertView;
            viewHolder = (ViewHolder)view.getTag();
        }
        viewHolder.fruitImage.setImageResource(fruit.getImageId());
        viewHolder.fruitName.setText(fruit.getName());
        return view;
    }
}

class ViewHolder{
    ImageView fruitImage;
    TextView fruitName;
}
```



通过上面两步的优化，ListView的运行效率提高了不少。

### 点击事件

修改MainActivity.java:

```java
listView.setOnItemClickListener((parent, view, position, id) -> {
    Fruit fruit = fruitList.get(position);
    Toast.makeText(MainActivity.this,fruit.getName(),
            Toast.LENGTH_SHORT).show();
});
```

效果如下：

<img src="04.png" width=480px>

