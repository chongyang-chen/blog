---
title: 结构体和共用体，位运算与预处理
date: 2018-01-05 19:34:33
tags: 
- C
- 结构体
categories:
- C
---

### 结构体
struct 结构体名
{
	成员列表
};


创建学生结构体：

```
struct Student
{
	char cName[20];//姓名
	int iAge;//年龄
};
```

指向结构体变量的指针：

```
struct Student *pStruct;
pStruct->age = 20;

```

使用结构体变量作为函数参数采用的值传递方式。

<!-- more -->
链表

```
struct Student
{
	char cName[20];
	int iNumber;
	struct Student* pNext;
};
```

创建动态链表

malloc函数，calloc函数，free函数。

```C
int iCount;
struct Student* Create()
{
	struct Student* pHead = NULL;
	struct Student* pEnd, *pNew;
	iCount = 0;
	pEnd = pNew = (struct Student*)malloc(sizeof(struct Student));
	printf("enter name and number:");
	scanf("%s", &pNew->cName);
	scanf("%d", &pNew->iNumber);
	while(pNew->iNumber != 0){
		iCount++;
		if(iCount == 1) {
			pNew->pNext = pHead;
			pEnd = pNew;
			pHead = pNew;
		
		} else {
			pNew->pNext = NULL;
			pEnd->pNext = pNew;
			pEnd = pNew;
		
		}
		pNew = (struct Student*)malloc(sizeof(struct Student));
		scanf("%s", &pNew->cName);
		scanf("%d", &pNew->iNumber);
	}
	free(pNew);
	
	return pHead;
}
```

链表的插入与删除


```
struct Student *Insert(struct Student *pHead)
{
	struct Student *pNew;
	pNew = (struct Student*)malloc(sizeof(struct Student));
	pNew->pNext = pHead;
	pHead = pNew;
	iCount++;
	return pHead;
}

void Delete(struct Student *pHead, int iIndex)
{
	int i;
	struct Student *pTemp;
	struct Student *pPre;
	pTemp = pHead;
	pPre = pTemp;
	for(i = 1; i<iIndex; i++)
	{
		pPre = pTemp;
		pTemp = pTemp->pNext;
	}
	pPre->pNext = pTemp->pNext;
	free(pTemp);
	iCount--;	
}
```

共用体定义了一块为所有数据成员共享的内存。

union 共用体名
{
	成员列表
}变量列表;

枚举类型

```
enum Colors(Red, Green, Blue);

```

位运算

一个字节通常是由8位二进制数组成的。
运算符：& | ～ ^ >> << >>>
不使用临时变量的情况下实现两个变量值的互换：


```
x = x ^ y;
y = y ^ x;
x = x ^ y;
```

循环左移，循环右移：
```
(value >> (32 - n)) | (value << n);
(value << (32 - n)) | (value >> n);
```

位段

```
struct status
{
	unsigned sign: 1;//符号标志
	unsigned zero: 1;//零标志
	unsigned carry: 1;//进位标志
	。。。

} flags;

```

预处理

宏定义

```
#define PI 3.141592653

```

\#include指令
一般将如下内容放到.h文件中：宏定义，结构，联合枚举声明，typedef声明，外部函数声明，全局变量声明。

条件编译

```
#if

#elif

#else

#endif

#ifdef

#ifndef


```

