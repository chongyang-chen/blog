---
title: Java Character 类
date: 2018-01-29 20:56:34
tags:
- Java
- 字符
categories:
- Java
---

Character 类用于对单个字符进行操作。

Character 类在对象中包装一个基本类型 char 的值。

```
char ch = 'a';
 
// Unicode 字符表示形式
char uniChar = '\u039A'; 
 
// 字符数组
char[] charArray ={ 'a', 'b', 'c', 'd', 'e' };
```

<!-- more -->
然而，在实际开发过程中，我们经常会遇到需要使用对象，而不是内置数据类型的情况。为了解决这个问题，Java语言为内置数据类型char提供了包装类Character类。

Character类提供了一系列方法来操纵字符。你可以使用Character的构造方法创建一个Character类对象，例如：

```
Character ch = new Character('a');
```
在某些情况下，Java编译器会自动创建一个Character对象。

例如，将一个char类型的参数传递给需要一个Character类型参数的方法时，那么编译器会自动地将char类型参数转换为Character对象。 这种特征称为装箱，反过来称为拆箱。

```
// 原始字符 'a' 装箱到 Character 对象 ch 中
Character ch = 'a';
 
// 原始字符 'x' 用 test 方法装箱
// 返回拆箱的值到 'c'
char c = test('x');
```

### 转义序列
前面有反斜杠（\）的字符代表转义字符，它对编译器来说是有特殊含义的。

下面列表展示了Java的转义序列：

|转义序列|	描述|
|:-----:|:-----:|
|\t	|在文中该处插入一个tab键|
|\b	|在文中该处插入一个后退键|
|\n	|在文中该处换行|
|\r	|在文中该处插入回车|
|\f	|在文中该处插入换页符|
|\'	|在文中该处插入单引号|
|\"	|在文中该处插入双引号|
|\\	|在文中该处插入反斜杠|

\r： return 到当前行的最左边。

\n： newline 向下移动一行，并不移动左右。

Linux中\n表示：回车+换行；

Windows中\r\n表示：回车+换行。

Mac中\r表示：回车+换行。

>历史：回车"（Carriage Return）和"换行"（Line Feed）这两个概念的来历和区别。 在计算机还没有出现之 前，有一种叫做电传打字机（Teletype Model 33，linux/Unix下的tty概念也来自于此）的玩意，每秒钟可以打10个字符。但是它有一个问题，就是打完一行换行的时候，要用去0.2秒，正 好可以打两个字符。要是在这0.2秒里面，又有新的字符传过来，那么这个字符将丢失。于是，研制人员想了个办法解决这个问题，就是在每行后面加两个表示结束的字符。一个叫做"回车(return)"，告诉打字机把打印头定位在左边界；另一个叫做"换行(newline)"，告诉打字机把纸向下移一行。这就是"换行"和"回车"的来历，从它们的英语名字上也可以看出一二。

当打印语句遇到一个转义序列时，编译器可以正确地对其进行解释。

以下实例转义双引号并输出：

Test.java 文件代码：

```
public class Test {
 
   public static void main(String args[]) {
      System.out.println("访问\"我的博客!\"");
   }
}
```
以上实例编译运行结果如下：

```
访问"我的博客!"
```

### Character 方法

下面是Character类的方法：

#### isLetter()
是否是一个字母

```
public class Test {

    public static void main(String args[]) {
        System.out.println(Character.isLetter('c'));
        System.out.println(Character.isLetter('5'));
    }
}
```
以上程序执行结果为：

```
true
false
```

#### isDigit()
是否是一个数字字符

```
public class Test {

    public static void main(String args[]) {
        System.out.println(Character.isDigit('c'));
        System.out.println(Character.isDigit('5'));
    }
}
```
以上程序执行结果为：

```
false
true
```

#### isWhitespace()
是否是一个空格

```
public class Test {

    public static void main(String args[]) {
        System.out.println(Character.isWhitespace('c'));
        System.out.println(Character.isWhitespace(' '));
        System.out.println(Character.isWhitespace('\n'));
        System.out.println(Character.isWhitespace('\t'));
    }
}
```
以上程序执行结果为：

```
false
true
true
true
```

#### isUpperCase()
是否是大写字母

```
public class Test {

    public static void main(String args[]) {
        System.out.println( Character.isUpperCase('c'));
        System.out.println( Character.isUpperCase('C'));
    }
}
```
以上程序执行结果为：

```
false
true
```

#### isLowerCase()
是否是小写字母

```
public class Test {

    public static void main(String args[]) {
        System.out.println( Character.isLowerCase('c'));
        System.out.println( Character.isLowerCase('C'));
    }
}
```
以上程序执行结果为：

```
true
false
```

#### toUpperCase()
指定字母的大写形式

```
public class Test {

    public static void main(String args[]) {
        System.out.println( Character.isLowerCase('c'));
        System.out.println( Character.isLowerCase('C'));
    }
}
```
以上程序执行结果为：

```
true
false
```

#### toLowerCase()
指定字母的小写形式

```
public class Test {

    public static void main(String args[]) {
        System.out.println(Character.toLowerCase('a'));
        System.out.println(Character.toLowerCase('A'));
    }
}
```
以上程序执行结果为：

```
a
a
```

#### toString()
返回字符的字符串形式，字符串的长度仅为1

```
public class Test {

    public static void main(String args[]) {
        System.out.println(Character.toString('a'));
        System.out.println(Character.toString('A'));
    }
}
```
以上程序执行结果为：

```
a
A
```
