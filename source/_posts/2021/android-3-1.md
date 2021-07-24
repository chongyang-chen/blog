---
title: android学习笔记（3-1）
categories:
  - android
tags:
  - android
date: 2021-02-25 20:35:17
---

今天来学习另一个重要的控件 Button。在上一章多次用到了它。
<!-- more -->

### Button

代码如下：

```xml
   <Button
        android:id="@+id/button"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Button" />
```

运行程序发现现实的大些 “BUTTON”，添加下面代码就行了。

```xml
android:textAllCaps="false"
```

添加按钮响应事件，点击按钮，输出信息，此处根据编辑器的提示优化了代码。

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button button = (Button)findViewById(R.id.button);
        button.setOnClickListener(v -> Log.d("MainActivity", "onClick: "));
    }
}
```

<img src="01.png" width=800px>

### EditText

```xml
<EditText
    android:id="@+id/edit_text"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:hint="Type something here"
    android:maxLines="2"/>
```

修改代码，点击按钮现实输入框的内容。

```java
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    Button button = (Button)findViewById(R.id.button);
    editText = (EditText)findViewById(R.id.edit_text);
    button.setOnClickListener(v -> {
        String textString = editText.getText().toString();
        Toast.makeText(this, textString, Toast.LENGTH_SHORT).show();
    });
}
```

效果如下：

<img src="02.png" width=480px>



### ImageView

首先新建文件夹 drawable-xhdpi，将准备好的两张图片放在该目录下。

```xml
<ImageView
    android:id="@+id/image_view"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:src="@drawable/img_1" />
```

点击按钮，修改图片。完整代码如下：

```java
public class MainActivity extends AppCompatActivity {

    private EditText editText;
    private ImageView imageView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Button button = (Button) findViewById(R.id.button);
        editText = (EditText) findViewById(R.id.edit_text);
        imageView = (ImageView) findViewById(R.id.image_view);
        button.setOnClickListener(v -> {
            imageView.setImageResource(R.drawable.img_2);
        });
    }
}
```

最终效果如下：

<img src="03.png" width=480px>