---
title: C语言核心技术
date: 2018-01-05 19:34:28
tags:
- C
categories:
- C
---
### 数组

一维数组的定义：类型说明符 数组标识符[常量表达式]；

二维数组的定义：数据类型 数组名 [常量表达式1] [常量表达式2]；
<!-- more -->

数组的排序算法

选择法排序

```
//从小到大排序
for(i = 0; i < 9; i++) {
	iTemp = a[i];//设置最小值
	iPos = i;//记录位置
	for(j = i + 1; j < 10; j++) {
		if(a[j < iTemp]) {
			iTemp = a[j];//重新设置最小值并记录元素位置
			iPos = j;
		}
		//交换元素位置
		a[iPos] = a[i];
		a[i] = iTemp;
	}
```
冒泡法排序

```
for(i = 1; i < 10; i++) {
	for(j = 9; j >= i; j--) {
	//如果前一个数比后一个数大，交换两个元素的位置
		if(a[j] < a[j-1]) {
			swap(a[j], a[j-1]);
		}
	}
}

```

交换法排序

```
for(i = 0; i < 9; i++) {
	for (j = i+1; j < 10; j++) {
		if(a[j] < a[i]) {
			swap(a[i], [j])
		}
	}
}
```

插入法排序

折半法排序（快速排序）递归实现。

对稳定性有要求是用插入或冒泡法排序。




### 函数

函数是构成C程序的基本单元。

函数的定义：函数头和函数体两部分。
函数头包括返回值类型，函数名，参数列表。
函数的声明：返回值类型 函数名（参数列表）；

内部函数与外部函数

static关键字将函数修饰成内部函数。

局部变量和全局变量。



### 指针

定义指针变量同时赋值。

```
int a;
int *p = &a;
```
定义指针变量后赋值。

```
int a;
int *p;
p = &a;
```

指向指针的指针： 类型标识符 **指针变量名；

指针变量作为函数参数：

```
void swap(int *a, int *b) {
	int temp;
	temp = *a;
	*a = *b;
	*b = temp;
}
int x = 10, y = 20;
swap(&x, &y);
```