---
title: java OOP基础知识
date: 2017-07-13 10:56:54
categories:
- Java
tags:
- Java
---

## 类

类是Java程序最基本的元素结构。

```java
class MyFirstClass {

}
```

对象是类的实例。对象一般通过实例化类创建。

```java
MyFirstClass object = new MyFirstClass();

```

<!-- more -->

类的成员一般包含字段和方法，也可以包括构造方法，初始化程序等。

```java
public class Dog {
	String breed;
	int age;
	String color;
	
	void barking(){
	}

	void sleeping() {
	}
	...
}

```

### 字段和方法
成员分为四类：类字段， 类方法， 实例字段， 实例方法。

一个简单的类及其成员.

```java
puclic class Circle {
	//类字段
	public static final double PI = 3.14159;
	//类方法
	public static double radiansToDegrees(double radians) {
		return radians * 180 / PI;
	}
	
	//构造方法
	public Circle(double r) {
		this.r = r;
	}
	
	public Circle() {
		this(1.0);
	}
	
	//实例字段
	public double r;
	//实例方法
	public double area() {
		return PI * r * r;
	}
	//实例方法
	public double circumference(){
		return 2 * PI * r;
	}


```

创建对象

```

Circle c1 = new Circle();
c1.r = 2.2;

Circle c2 = new Circle(2.2);

```

### 字段的默认值和初始化程序

#### 静态初始化程序

```java
static {
	//初始化代码
}

```

#### 实例初始化程序

```java
{
	//初始化代码
}

```

## 子类和继承

```java

public class PlaneCircle extends Circle {
	//继承父类的字段和方法，可以添加自己的方法和字段。

}


```
### 类的层次结构
类的层次结构类似一个树状图，根为 Object 类。

1. 它是 Java 中唯一一个没有超类的类。
2. 所有 Java 类都从 Object 类中继承方法。

### 遮盖超累的字段与覆盖超类的方法。
为字段命名时应该避免遮盖超类的字段，子类可以根据需要覆盖父类的方法，使用 super 语法可以调用被覆盖的父类方法。

### 数据的隐藏和封装

1. 如果内部字段和方法对外可见，会弄乱类的API，让可见的字段尽量少，可以保持类的整洁，易于使用和理解。
2. 如果方法对类的使用者可见，就要为其编写文档。把方法隐藏起来，可以节省编写文档的时间，用这些时间做些更有意义的事吧。 













