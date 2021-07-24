---
title: C语言入门
date: 2018-01-05 18:48:09
tags:
- C
categories:
- C
---

### 标志符
C语言标识符以字母或下划线开头，后跟数字，字母下划线，标志符区分大小写，并且不能是关键字，最好具有相关的含义。

<!-- more -->

### C语言关键字
|auto|double|int|struct|break|else|
|:---:|:---:|:---:|:----:|:-------:|:----:|
|long|switch|case|enum|register|typedef|
|char|extern|union|return|const|float|
|short|unsigned|continue|for|signed|void|
|default|goto|sizeof|volatile|do|while|
|static|if|

### 数据类型
#### 基本类型

整型，字符型，浮点型，枚举类型。

#### 构造类型
数组类型，结构体类型，共用体类型。

#### 指针类型

#### 空类型

### 变量的存储类型
具体主要由四种：auto，static，register，extern。

### 运算符
赋值运算符： = ；

常数不能作为左值。 

算数运算符： +， -， *， /，% ；

自增，自减运算符： ++， -- ；

关系运算符：>, >=, <, <=, ==, != ；

注意区分 == 与 = 的区别。

逻辑运算符： &&，||， ！

注意出现短路的情况。

位逻辑运算符： &，|，^, ~

逗号运算符： ，

符合复制运算符： += 

三目运算符： ？：

