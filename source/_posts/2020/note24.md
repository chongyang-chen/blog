---
title: Java学习笔记(二)
tags:
  - java
categories:
  - note
  - java
date: 2020-01-02 18:52:07
---
## 第四章 流程控制

今天是2020年第一次开始java学习，继续学习第四章的内容。这章的内容和C语言差不多，学起来也比较容易。

<!-- more -->

## 复合语句 
复合语句是在`{...}`之间的语句，复合语句可以嵌套其他复合语句。复合语句为局部变量创建了一个作用域，作用域外局部变量无法使用。

## 条件语句

### if 语句

语法如下：

```java
if(表达式){
	//do something
}
```
当if表达式后只有一条语句时，大括号`{}`可以省略。
书中说明：为了增强程序的可读性最好不要省略。在不影响程序可读性的情况下，是可以省略的。

### if...else语句

语法如下：

```java
if(表达式){
	语句块1
} else {
	语句块2
}
```
if...else语句可以使用三目运算符进行简化，

### if...else if语句
语法格式：

```java
if(表达式1){
	语句块1
}else if(表达式2){
	语句块2
}...
else if(表达式n){
	语句块n
}
```
针对于某一事件的多种情况进行处理，比如视频平台可以分为普通用户，vip用户，svip用户，vvip用户等。

### switch多分支语句

switch语句和`if...else if`语句在功能上类似，但使用起来更加方便。switch语句中表达式类型，可以是 **整型，字符型或者字符串类型**。

## 循环语句

java中有三种常用的循环语句，while，do...while和for循环语句，这点和C语言十分类似。使用循环可以快速计算出从1加到100的值，同样也能快速计算从99加到9999。只需要修改初始值和结束值就可以了。如果用计算器需要算很久。计算机每秒可以处理很多的运算量，可以帮助我们做很多的事情。
### 循环控制
控制循环的跳转需要用到 **break** 和 **continue** 这两个关键字。break 和 continue 支持跳转到指定标签的功能，对于初学者而言，了解即可。

## 第五章 字符串

字符串作为单独的一章来学习，可见java中字符串的重要性。学好字符串，对于编程至关重要。

## String 类
Java 中字符串作为String类的对象来处理。
### 字符串声明

```java
String str;
```

### 创建字符串

```java
String str;
str = "We are students";
```
书中讲解了创建字符串的其他方法，作为初学者的我，喜欢上面的方法。

## 拼接字符串
字符串拼接是字符串操作中较简单的一种。

### 连接多个字符串
使用 `+`运算符可以连接多个字符串并产生一个新的String对象。

### 连接其他数据类型
对于其他数据类型，连接时会自动调用`toString()`方法，然后再与字符串连接。

## 获取字符串信息

### 字符串长度

length()方法可以获取字符串对象的长度。

### 字符串查找

字符串下标是0 ~ length()-1，注意下标是从0开始的。至于为什么从0开始，而不是从1开始，相信网上能够找到比较合理的解释。`indexOf(),lastIndexOf()`这两个方法可以查找指定字符或者字符串的位置。

### 获取指定位置的字符

语法如下：

```java
str.charAt(int index)
```

## 字符串操作
下面是几种常见的字符串操作，更多的操作可以查看Java API进行学习。

```java
1. substring()
2. strim() 去除空格
3. replace()字符串替换
4. startsWith()
5. endsWith()
6. equals()比较字符串是否相等
7. equalsIgnoreCase()忽略大小写
8. compareTo()按字段顺序比较两个字符串
9. toLowerCase()
10. toUpperCase()
11. split()字符串分割，可以使用正则表达式
```


## 格式化字符串

### 日期和时间字符串格式化
在程序这几种，经常需要显示时间和日期，format()方法可以输出你想要的日期和时间格式。比如：`2020-01-02 20:29:37`

```java
Date date = new Date();
String time = String.format("%tF %tT", date, date);
System.out.println(time);
```

#### 日期格式化 

```java
1. %te 一个月中的某一天
2. %tb 月份简称
3. %tB 月份全称
4. %tA 星期几全称
5. %ta 星期几简称
6. %tc 显示日期和时间全部信息
7. %tY 4位年份 2020
8. %ty 2位年份 20
9. %tj 一年中的第几天 001-366
10. %tm 月份 01-12
11. %td 一个月中的第几天 01-31
```

```java
Date date = new Date();
String time;
time = String.format("%te", date);
System.out.println("今天是这个月的第" + time + "天。");

time = String.format("%ta", date);
System.out.println("今天是" + time);

time = String.format("%tA", date);
System.out.println("今天是" + time);

time = String.format("%tB", date);
System.out.println("今天是" + time);

time = String.format("%tb", date);
System.out.println("今天是" + time);

time = String.format("%tc", date);
System.out.println("今天是" + time);

time = String.format("%tY", date);
System.out.println("今年是" + time + "年");

time = String.format("%tj", date);
System.out.println("今天是今天的第" + time+"天");

time = String.format("%tm", date);
System.out.println("今天是" + time+ "月");

time = String.format("%td", date);
System.out.println("今天是这个月的第" + time + "天");

time = String.format("%ty", date);
System.out.println("今天年是" + time + "年");
```
输出结果：

```
今天是这个月的第2天。
今天是Thu
今天是Thursday
今天是January
今天是Jan
今天是Thu Jan 02 21:41:27 CST 2020
今年是2020年
今天是今天的第002天
今天是01月
今天是这个月的第02天
今天年是20年
```
下面是下面是一些英文日期的单词。

> 一月：January 二月：February 三月：March 四月：April 五月：May 六月：June 七月：July 八月：August 九月：September 十月：October 十一月：November 十二月：December

> 周一：Monday
周二：Tuesday
周三：Wednesday
周四：Thursday
周五：Friday
周六：Saturday
周日：Sunday


> 以下为简写
星期一 Mon.
星期二 Tue.
星期三 Wed.
星期四 Thu.
星期五 Fri.
星期六 Sat.
星期天 Sun.

#### 时间格式化
时间格式化比日期格式化更多，更准确。可以将时间格式化为时，分，秒，毫秒。其中：1小时=60分，1分=60秒，1小时=3600秒。

```java
1. %tH  2位数字的24时制的小时，00-23
2. %tI  2位数字的12时制的小时，01-12
3. %tk  2位数字的24时制的小时，0-23
4. %tl  2位数字的12时制的小时，1-12
5. %tM  2位数字的分钟
6. %tS  2位数字的秒数
7. %tL  3位数字的毫秒数
8. %tN  9位数字的微秒数
9. %tp  上午或下午
10. %tz 时区偏移量
11. %tZ 时区缩写字符串
12. %ts 1970-01-01 00：00：00至今经过的秒数
13. %tq 1970-01-01 00：00：00至今经过的毫秒数
```

```java
Date date = new Date();
String time;
time = String.format("%tH", date);
System.out.println("现在是" + time);

time = String.format("%tI", date);
System.out.println("现在是" + time);
time = String.format("%tk", date);
System.out.println("现在是" + time);
time = String.format("%tl", date);
System.out.println("现在是" + time);
time = String.format("%tM", date);
System.out.println("现在是" + time);
time = String.format("%tS", date);
System.out.println("现在是" + time);
time = String.format("%tL", date);
System.out.println("现在是" + time);
time = String.format("%tN", date);
System.out.println("现在是" + time);
time = String.format("%tp", date);
System.out.println("现在是" + time);
time = String.format("%tz", date);
System.out.println("现在是" + time);
time = String.format("%tZ", date);
System.out.println("现在是" + time);
time = String.format("%ts", date);
System.out.println("现在是" + time);
time = String.format("%tQ", date);
System.out.println("现在是" + time);

```

输出结果：

```
现在是21
现在是09
现在是21
现在是9
现在是59
现在是31
现在是165
现在是165000000
现在是pm
现在是+0800
现在是CST
现在是1577973571
现在是1577973571165
```

#### 常见的日期时间组合

下面是常用的日期和时间的组合格式：

```java
1. %tF 2020-01-01
2. %tD `月/日/年` 格式，2位年份（03/01/20）
3. %tc 全部日期和时间信息
4. %tr `时:分:秒`12时制
5. %tT `时:分:秒`24时制
6. %tR `时:分`24时制
```

```java
Date date = new Date();
String time;
time = String.format("%tF", date);
System.out.println("现在是" + time);
time = String.format("%tD", date);
System.out.println("现在是" + time);
time = String.format("%tc", date);
System.out.println("现在是" + time);
time = String.format("%tr", date);
System.out.println("现在是" + time);
time = String.format("%tT", date);
System.out.println("现在是" + time);
time = String.format("%tR", date);
System.out.println("现在是" + time);
```
输出结果:

```
现在是2020-01-07
现在是01/07/20
现在是Tue Jan 07 17:55:42 CST 2020
现在是05:55:42 PM
现在是17:55:42
现在是17:55
```

以上就是日期和时间字符串格式化的全部内容，很难都记住。记录下来，方便以后查看😀。

### 常规类型格式化

1. %b, %B 布尔类型
2. %h, %H 散列码
3. %s, %S 字符串类型
4. %c, %C 字符类型
5. %d     十进制整数
6. %o     八进制整数
7. %x, %X 16进制整数
8. %e	    科学计数法表示的十进制数
9. %a     带有有效位数和指数的十六进制数
10. %n    特定于平台的行分隔符
11. %%    字面值`%`


## 正则表达式

### 正则表达式中的元字符：

```java
1. . 代表任意字符
2. \d 代表0-9任何一个数字
3. \D 代表任何一个非数组
4. \s 代表空白字符
5. \S 代表非空白字符
6. \w 代表可用户标识符的字符，不包括“$”
7. \W 代表不可用户标识符的字符
```

其中`"."`代表任何一个字符，想要使用普通意义的点字符`“.”`，请使用转义字符`“\”`。

### 正则表达式中的限定修饰符

```java
1. ？ 0次或1次
2. *  0次或多次
3. +  1次或多次
4. {n} 正好n次
5. {n,} 至少n次
6. {n.m} n-m次
```

### 例子

判断字符串是否是合法的邮箱地址：`"\\w+@\\w+(\\.\\w{2,3})*\\.\\w{2,3}"`
一般邮箱格式为：`X@X.com.cn` X表示任意的一个或多个字符。

分析：`\\w`代表任意字符，`+`表示字符可以出现一次或多次。`(\\.\\w{2,3})*`表示形如`.com`格式的字符串可以出现0次或多次。

## 字符串生成器

频繁的附加字符串，建议使用StringBuilder，可以动态的执行添加，删除，插入等字符串的编辑操作。

精通Java中的字符串处理基础是学习Java语言的基础，格式化字符串，使用正则表达式等，这些内容是字符串处理技术的重点，应该熟练掌握。

## 第六章 数组

数组是一种常见的数据结构，数组对java编程同样十分重要。接下来开始学习数组，与C语言中的数组十分相似。

## 数组概述

数组是一组具有相同数据类型的数据的集合。根据数组的维数可将数组分为一维数组，二维数组...

## 一维数组的创建和使用

### 声明语法

```
元素类型 数组名字[]
元素类型[] 数组名字
```
比如：

```java
int arr[];
String str[];
```
### 分配内存

```java
arr = new int[10];
```
可以将数组的声明和内存分配放在一起：

```java
int months[] = new int[12];
```

### 初始化

```java
int arr[] = new int[]{1, 2, 3, 4, 5};
int arr2[] = {1, 2, 3, 4, 5, 6, 7, 8};
```
注意：数组下标是从0开始的。

## 二维数组的创建和使用
同一维数组类似，同样包括声明，分配内存，和初始化等内容。作为初学者，掌握一维数组即可。

## 数组的基本操作

java.util包的Arrays类包含了各种操作数组的方法。

### 数组遍历

```java
int arr[] = {1, 2, 3, 4, 5};
for (int a : arr){
    System.out.println(a);
}
```
注意foreach的语法格式使用的是 `“:”`。

### 填充替换数组元素

```java
int arr[] = new int[5];
Arrays.fill(arr, 6);
Arrays.fill(arr, 2, 4, 9);
for (int a : arr){
    System.out.println(a);
}
```

### 数组排序

`Arrays.sort(ojb)`

### 数组复制

```java
int arr[] = {1, 2, 3};
int newArr[] = Arrays.copyOf(arr, 4);
for (int a : newArr){
    System.out.println(a);
}
System.out.println();
int newArr2[] = Arrays.copyOfRange(arr, 0, 4);
for (int a : newArr2){
    System.out.println(a);
}
```
### 数组查询
Arrays类的binarySearch()方法，可以使用二分查找方法来查找指定数组，注意数组先排序才能使用此方法。排序与查找是数据结构的基本算法。

## 数组排序算法
冒泡排序，直接选择排序，反转排序。排序属于数据结构中的知识，以后专门来学习排序相关的算法。作为初学者，先暂时跳过者一节👌。




