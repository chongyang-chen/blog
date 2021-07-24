---
title: C语言学习笔记（十二）
tags:
  - C
categories:
  - C
date: 2018-07-14 11:39:59
---

到目前为止，只学习了基本类型，无法满足各种复杂程序的要求，C语言提供了构造类型的数据，结构体和共用体。在C语言编程中，首先用typedef定义程序中用到的数据类型，然后用定义的数据类型定义程序中用到的数据结构。

<!-- more -->

```C
#include <stdio.h>
#include <string.h>

typedef int StudentAgeType;
typedef char StudentNameType[20];

struct Student{
    StudentAgeType age;
    StudentNameType name;
}stu;

int main(int argc, const char * argv[]) {
    StudentAgeType age = 20;
    StudentNameType name = "LiLei";
    stu.age = age;
    strcpy(stu.name, name);
    printf("%s is %d years old.\n", stu.name, stu.age);
}

//LiLei is 20 years old.
```

结构体的成员列表可以包含其他结构体类型，不能包含结构体自身类型的变量，可以包含自身类型的指针变量。比如链表。
可以声明指向结构体的指针，也可以声明结构体数组。
访问结构体的成员 使用 . 运算符。

```
struct Student *pStu;
pStu = &stu;
stu.age = 20;
(*pStu).age = 10;
pStu->age = 20;
```
当结构体指针变量访问结构体成员时，可以使用 -> 运算符。

**记住：**. -> () [] 这四个运算符的优先级是最高的，结合性自左向右的。

指向结构体数组的指针和指向数组的指针类似，数组类型从基本类型变成了结构体类型。

结构体作为函数测参数采用的是“值传递”，当结构体很复杂时，这种传递方式在空间和时间上开销都比较大。此外，函数内修改成员的值，对主调函数不影响。一般地，更习惯使用结构体变量的指针作为函数的参数。
包含结构的结构，可以定义更加复杂的数据类型。
有关链表的知识，学习数据结构的时候再来深入的学习。

共用体

共用体也称联合体，它是几种不同类型的变量存放到同一段内存单元中，同一时刻只能有一个值，共用体的大小等于最大成员的大小。

枚举类型

使用枚举类型可以定义枚举变量，一个枚举变量包含一组相关的标识符，每个标识符都对应一个整数值，称为枚举常量。
比如

```
enum Colors(red, green, blue);
```




