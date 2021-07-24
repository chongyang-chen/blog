---
title: 数据结构学习笔记（三）
categories:
  - data struct
tags:
  - 数据结构
date: 2018-07-31 19:11:09
---

指针是C语言的一个重要概念，也是最不容易掌握的内容，今天来学习一下C语言指针。
<!-- more -->

指针与数组

指向数组元素的指针

```C
int main(int argc, const char * argv[]) {
  
    
    int q = 12;
    int *qPtr;
    qPtr = &q;
    printf("&q = %p\n", qPtr);
    printf("&qPtr = %p\n", &qPtr);
   //    &q = 0x7ffeefbff63c
   // &qPtr = 0x7ffeefbff630
    
    //指针与数组。
    int a[5] = {10, 20, 30, 40, 50};
    int *aPtr, i;
    aPtr = a;//指针指向数组首元素的地址。
    for (i = 0; i < 5; i++) {
        printf("a[%d] = %d\n", i, a[i]);
    }
    for (i = 0; i < 5; i++) {
        printf("*(a+%d) = %d\n", i, *(a+i));
    }
    for (i = 0; i < 5; i++) {
        printf("aPtr[%d] = %d\n", i, aPtr[i]);
    }
    for (i = 0; i < 5; i++) {
        printf("*(aPtr+%d) = %d\n", i, *(aPtr+i));
    }
    return 0;
}
```
在C语言中指针的应用十分灵活。

指针数组

```
char *s[4] = {"C","Programming","Language","!"};
```
数组指针

```
int (*p)[4];//括号不能省略。
int a[3][4] = {{1, 2, 3, 4},{5, 6, 7, 8},{9, 10, 11, 12}};
p = a;
```
p是一个指针，是指向一个数组的指针，数组有4个整型元素。a是一个二维数组，p指向了二维数组首元素的地址。*(p+1)+2表示&a[1][2],

指针函数与函数指针

指针函数是指函数的返回值是指针类型的函数。
```
int *func(int a, int b);
```
函数指针

```
int (*func)(int, int);
//func是一个指针，指向函数的指针，该函数返回整型，并且有两个参数。
```
函数指针可以作为函数的参数，也可以定义函数指针数组。
在C语言中，函数的参数传递的方式一般有两种：传值和传地址。

结构体和联合体

联合体变量是可以作为函数的参数的，在有的教科书上说的是不可以，只能说C语言本身也是在不断完善的，一些知识要通过实践来验证。



