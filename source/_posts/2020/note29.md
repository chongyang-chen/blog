---
title: Java String
date: 2018-01-29 20:44:26
tags:
- Java
- 字符串
categories:
- Java
---
字符串广泛应用在 Java 编程中，在 Java 中字符串属于对象，Java 提供了 String 类来创建和操作字符串。

<!-- more -->

### 创建字符串

创建字符串最简单的方式如下:

```
String greeting = "Java教程";
```
在代码中遇到字符串常量时，这里的值是 "Java教程"，编译器会使用该值创建一个 String 对象。

和其它对象一样，可以使用关键字和构造方法来创建 String 对象。

String 类有 11 种构造方法，这些方法提供不同的参数来初始化字符串，比如提供一个字符数组参数:

StringDemo.java 文件代码：

```
public class StringDemo{
   public static void main(String args[]){
      char[] helloArray = { 'H', 'e', 'l', 'l', 'o', '!'};
      String helloString = new String(helloArray);  
      System.out.println( helloString );
   }
}
```
以上实例编译运行结果如下：

```
Hello!
```
>注意: **String** 类是不可改变的，所以你一旦创建了 String 对象，那它的值就无法改变了。

如果需要对字符串做很多修改，那么应该选择使用 StringBuffer & StringBuilder 类。

### 字符串长度
用于获取有关对象的信息的方法称为访问器方法。

String 类的一个访问器方法是 length() 方法，它返回字符串对象包含的字符数。

下面的代码执行后，len变量等于14:

StringDemo.java 文件代码：

```
public class StringDemo {
    public static void main(String args[]) {
        String site = "www.ccyag.com";
        int len = site.length();
        System.out.println( "我的博客网址长度 : " + len );
   }
}
```

以上实例编译运行结果如下：

```
菜鸟教程网址长度 : 13
```

### 连接字符串
String 类提供了连接两个字符串的方法：

string1.concat(string2);
返回 string2 连接 string1 的新字符串。也可以对字符串常量使用 concat() 方法，如：

```
"我的名字是 ".concat("ccyag");
```

更常用的是使用'+'操作符来连接字符串，如：

```
"Hello," + " cccyag" + "!"
```

结果如下:

```
"Hello, ccyag!"
```

下面是一个例子:

StringDemo.java 文件代码：

```
public class StringDemo {
    public static void main(String args[]) {     
        String string1 = "我的博客网址：";     
        System.out.println("1、" + string1 + "www.ccyag.com");  
    }
}
```

以上实例编译运行结果如下：

```
1、我的博客网址：www.ccyag.com
```

### 创建格式化字符串

我们知道输出格式化数字可以使用 printf() 和 format() 方法。

String 类使用静态方法 format() 返回一个String 对象而不是 PrintStream 对象。

String 类的静态方法 format() 能用来创建可复用的格式化字符串，而不仅仅是用于一次打印输出。

如下所示：

```
System.out.printf("浮点型变量的值为 " +
                  "%f, 整型变量的值为 " +
                  " %d, 字符串变量的值为 " +
                  "is %s", floatVar, intVar, stringVar);
```

你也可以这样写：

```
String fs;
fs = String.format("浮点型变量的值为 " +
                   "%f, 整型变量的值为 " +
                   " %d, 字符串变量的值为 " +
                   " %s", floatVar, intVar, stringVar);
```