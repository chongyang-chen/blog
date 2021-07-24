---
title: Java学习笔记(三)
tags:
  - java
categories:
  - note
  - java
date: 2020-01-08 18:49:37
---

今天开始java类和对象的学习。
<!-- more -->
## 第七章 类和对象

掌握类和对象是学习java的基础。
## 面向对象概述

面向对象设计实质上是对现实世界的对象进行建模操作。

### 对象
对象是事物存在的实体，比如手机，电脑，等。对象包含静态部分和动态部分，静态部分被称为属性，动态部分是对象具备的行为。比如一只大雁，有一对翅膀，一双脚。可以飞行和跳跃。前者是属性，后者是大雁的行为。

### 类

类是同一类事物的统称，比如鸟类，人类等。在Java中，类的对象行为是以方法的形式定义的。类的属性是以成员变量的形式定义的。类包括了对象的属性和方法。

### 面向对象特点

面向对象程序设计具有以下特点：封装，继承与多态。

## 类
下面将要学习类在java中是如何定义的。这是本章的重点内容。
### 成员变量，成员方法

下面的代码定义了一个图书类，包括一个成员变量，和三个成员方法。

```java
public class Book {
    private String name;

    public String getName(){

        setName("Java从入门到精通(第四版)");
        return this.name;
    }

    private void setName(String name){
        this.name = name;
    }

    public Book getBook(){
        return this;
    }
}
```

### 权限修饰符
java中权限修饰符有三种： **private，protected，public**。private 仅在本类中可见，public 都可见。

### 局部变量以及有效范围

在成员方法内定义的变量称为局部变量，它的有效范围从声明开始，到结束为止。在有效范围之外使用局部变量是错误的。

### this关键字

this关键字用来代表本类对象的引用，this可以调用成员变量和成员方法，还可以作为方法的返回值。

## 构造方法

类实例化对象时，会自动调用构造方法。
构造方法没有返回值，同时构造方法名称与类名相同。没有定义构造方法时，编译器会自动创建一个不带参数的构造方法。一般的，编程中都会编写类的构造方法，在构造方法中为成员变量赋值。

## 静态变量，方法和常量

**static** 关键字，表示静态的意思。语法如下：

```
类名.静态成员
```
注意：静态方法中不可以使用this，不可以直接调用非静态方法。

不能将局部变量声明为static。可以使用static定义一个静态区域，该区域将首先执行，且只会执行一次。

## 类的主方法
主方法是java程序的入口，语法如下：

```java
public static void main(String[] args) {
// write your code here
}
```
程序运行时可以提供参数，主方法以数组形式接收这些参数，主方法无返回值，且是`public static`的。

## 对象
java中所有的问题都通过对象来处理，下面就来学习对象在java中的应用。

### 对象的创建

语法如下：

```java
Book book = new Book();
```
java中对象和实例其实是一回事。习惯上使用类和对象。
创建对象的时候自动调用构造方法。

```java
public class Book {
    private String name;
    private float price;

    public Book(){
    }

    public Book(String name, float price){
        this.setName(name);
        this.setPrice(price);
    }

    public String getName(){
        return this.name;
    }

    public void setName(String name){
        this.name = name;
    }

    public float getPrice() {
        return this.price;
    }

    public void setPrice(float price){
        this.price = price;
    }

    public void showPrice(){
        System.out.println(String.format("《%s》的价格是%.2f元。", this.getName(),
                this.getPrice()));
    }

    public static void main(String[] args) {
        // write your code here
        Book book = new Book();
        book.setPrice(69.6f);
        book.setName("Java从入门到精通(第四版)");
        Book book1 = new Book("Java从入门到精通(第六版)",89.6f);
        book.showPrice();
        book1.showPrice();
    }
}
```
上面的代码创建了一个图书类，包含成员变量书名和价格，定义了一个方法用来输出图书的价格。预测这本书第六版的价格为80多元。

### 对象的引用

引用只是存放对象的内存地址，并非存放一个对象。
`Book book = new Book();` 可以理解成book是类Book对象的一个引用，指向对象的内存地址，类似于C语言的指针。

### 对象的比较

```java
String c1 = new String("abc");
String c2 = new String("abc");
System.out.println(String.format("%b", c1==c2));
System.out.println(String.format("%b", c2.equals(c1)));
```
上面创建了两个字符串对象，c1和c2指向不同的内存地址，所以他们是不相等的。

### 对象的销毁

对象都有生命周期，当对象生命周期结束时，对象占用的内存将会被回收，这就是java内存管理。Java中对象引用超过其作用范围，或者将对象引用赋值为null，这个对象将被视为垃圾。java垃圾回收机制将会回收这些内存。对于初学者，了解即可。

## 第八章 包装类

java为每种基本类型都提供了包装类，便于把基本类型转换为类对象来处理。下面学习java中的各种包装类。

java中Integer类，Long类，Short类，分别将int，long，short封装成一个类。

