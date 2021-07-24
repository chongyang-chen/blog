---
title: 学习笔记之C语言（1）
date: 2010-11-04 19:21:14
categories:
- C语言
tags:
- C语言
---

## 入门

一个简单的程序输出 Hello world！

```c
#include <stdio.h>

int main(int argc, const char * argv[]) {
    // insert code here...
    printf("Hello, World!\n");
    return 0;
}
```

<!-- more -->

## 变量与算数表达式

使用公式°C=(5/9)(°F-32)打印下列华氏温度与摄氏温度对照表：

```c
int main(int argc, const char * argv[]) {
//    使用公式°C=(5/9)(°F-32)打印下列华氏温度与摄氏温度对照表
    double f, c;
    double l, u, s;
    l = 0; u = 120; s = 5;
    f = l;
    while (f <= u) {
        c = 5 * (f-32) / 9;
        printf("%4.0f 华氏度等于 %.2f 摄氏度。\n", f, c);
        f += s;
    }
    return 0;
}
```

输出结果：

```c
   0 华氏度等于 -17.78 摄氏度。
   5 华氏度等于 -15.00 摄氏度。
  10 华氏度等于 -12.22 摄氏度。
  15 华氏度等于 -9.44 摄氏度。
  20 华氏度等于 -6.67 摄氏度。
  ...
```

使用公式°F=°C * 9 / 5 + 32打印下列华氏温度与摄氏温度对照表:

```c
int main(int argc, const char * argv[]) {
//    使用公式°F=°C * 9 / 5 + 32打印下列华氏温度与摄氏温度对照表
    double f, c;
    double l, u, s;
    l = 0; u = 120; s = 5;
    c = l;
    while (c <= u) {
//        c = 5 * (f-32) / 9;
        f = c * 9 / 5 + 32;
        printf("%4.0f 摄氏度等于 %4.0f 华氏度。\n", c, f);
        c += s;
    }
    return 0;
}
```

输出结果：
```c
   0 摄氏度等于   32 华氏度。
   5 摄氏度等于   41 华氏度。
  10 摄氏度等于   50 华氏度。
  15 摄氏度等于   59 华氏度。
  20 摄氏度等于   68 华氏度。
  ...
```

## for语句

```c
for (double f = 0; f <= 120; f += 5) {
    printf("%4.0f 华氏度等于 %.2f 摄氏度。\n", f, (5 / 9.0) * (f - 32));
}

for (double f = 120; f >= 0; f -= 5) {
    printf("%4.0f 华氏度等于 %.2f 摄氏度。\n", f, (5 / 9.0) * (f - 32));
}
```

## 符号常量 #define

符号常量通常以大写字母拼接，末尾没有分号。

```c
#define LOWER 0 /* 最低温度 */
#define UPPER 120 /* 最高温度 */
#define STEP 5 /* 步长 */
/* 打印华氏温度与摄氏温度对照表 */
int main(int argc, const char * argv[]) 
{
    for (double f = LOWER; f <= UPPER; f += STEP){
        printf("%4.0f 华氏度等于 %.2f 摄氏度。\n", f, (5 / 9.0) * (f - 32));
    }
    return 0;
}
```

## 字符输入/输出

### 文件复制

```c
int main(int argc, const char * argv[])
{
    int c;
    while ((c = getchar()) != EOF) putchar(c);
    return 0;
}
```

复制文件 main.c 到main.cc

```c
$ cc main.c 
$ ./a.out < main.c > main.cc
```

### 统计字符

```c
int main(int argc, const char * argv[])
{
    long nc = 0;
    while (getchar() != EOF)
        ++nc;
    printf("%ld\n", nc);
}
```

计算 main.c 文件字符数：

```C
$ cc main.c 
$ ./a.out < main.c
1935
```

### 行计数

```c
int main(int argc, const char * argv[])
{
    int c, nl;
    nl = 0;
    while ((c = getchar()) != EOF)
    if (c == '\n') ++nl;
    printf("%d\n", nl);
}
```

计算 main.c 文件一共有多少行：

```c
$ cc main.c
$ ./a.out < main.c
80
```

main.c 文件一共有80行，1935个字符。

编写一个将输入复制到输出的程序，并将其中连续的多个空格用一个空格代替。

```c
int main(int argc, const char * argv[]){
    int c;
    int inspace;
    inspace = 0;
    while((c = getchar()) != EOF) {
        if(c == ' ') {
            if(inspace == 0) {
                inspace = 1;
                putchar(c);
            }
        }
        if(c != ' ') {
            inspace = 0;
            putchar(c);
        }
    }
}
```

### 单词计数

```c
#define IN 1 /* inside a word */
#define OUT 0 /* outside a word */

int main(int argc, const char * argv[]){
    int c, nl, nw, nc, state;
    state = OUT;
    nl = nw = nc = 0;
    while ((c = getchar()) != EOF) {
        ++nc;
        if (c == '\n')
            ++nl;
        if (c == ' ' || c == '\n' || c == '\t')
            state = OUT;
        else if (state == OUT) {
            state = IN;
            ++nw;
        }
    }
    printf("一共有%d行 %d个单词 %d个字符。\n", nl, nw, nc);
}
```

统计 main.c 文件的单词数量。

```c
$ cc main.c
$ ./a.out < main.c 
一共有119行 512个单词 3012个字符。
```

## 数组

```c
int main(int argc, const char * argv[]){
    
    int c, i, nwhite, nother;
    int ndigit[10];
    nwhite = nother = 0;
    for (i = 0; i < 10; ++i)
        ndigit[i] = 0;
    while ((c = getchar()) != EOF){
        if (c >= '0' && c <= '9')
            ++ndigit[c-'0'];
        else if (c == ' ' || c == '\n' || c == '\t')
            ++nwhite;
        else
            ++nother;
    }
    printf("数组0-9 =");
    for (i = 0; i < 10; ++i)
        printf(" %d", ndigit[i]);
    printf(", 空白字符 = %d, 其他字符 = %d\n", nwhite, nother);
}
```

统计 main.c 不同种类的字符数。

```c
$ cc main.c
$ ./a.out < main.c
数组0-9 = 42 12 18 7 7 12 0 0 0 9, 空白字符 = 1234, 其他字符 = 2263
```

编写一个程序，打印输入中各个字符出现频度的直方图:

```c
#include <stdio.h>
#include <ctype.h>
#define NUM_CHARS 256
int main(void) {
    int c;
    long freqarr[NUM_CHARS + 1];
    long thisval = 0;
    long maxval = 0;
    int thisidx = 0;
    for(thisidx = 0; thisidx <= NUM_CHARS; thisidx++) {
        freqarr[thisidx] = 0;
    }
    while((c = getchar()) != EOF) {
        if(c < NUM_CHARS) {
            thisval = ++freqarr[c];
        }
        else
        {
            thisval = ++freqarr[NUM_CHARS];
        }
        if(thisval > maxval)
        {
            maxval = thisval;
        }
    }
    
    for(thisval = maxval; thisval > 0; thisval--) {
        printf("%4ld||", thisval);
        for(thisidx = 0; thisidx <= NUM_CHARS; thisidx++) {
            if(freqarr[thisidx] >= thisval) {
                printf("X");
            }
            else if(freqarr[thisidx] > 0) {
                printf(" ");
            }
        }
        printf("\n");
    }
    
    printf("     +");//5 spaces
    for(thisidx = 0; thisidx <= NUM_CHARS; thisidx++) {
        if(freqarr[thisidx] > 0) {
            printf("-");
        }
    }
    printf("\n      ");//6 spaces
    for(thisidx = 0; thisidx < NUM_CHARS; thisidx++) {
        if(freqarr[thisidx] > 0) {
            if (thisidx >= 100) {
                printf("%d", thisidx / 100);
            } else {
                printf(" ");
            }
        }
    }
    printf("\n      ");//6 spaces
    for(thisidx = 0; thisidx < NUM_CHARS; thisidx++) {
        if(freqarr[thisidx] > 0) {
            printf("%d",thisidx / 10 % 10);
        }
    }
    printf("\n      ");//6 spaces
    for(thisidx = 0; thisidx < NUM_CHARS; thisidx++) {
        if(freqarr[thisidx] > 0) {
            printf("%d", thisidx % 10);
        }
    }
    printf("\n      ");//6 spaces
    
    for(thisidx = 0; thisidx < NUM_CHARS; thisidx++) {
        if(freqarr[thisidx] > 0) {
            if (isprint(thisidx)){
                printf("%c",thisidx);
            } else {
                printf(" ");
            }
        }
    }
    
    if(freqarr[NUM_CHARS] > 0) {
        printf(">%d\n", NUM_CHARS);
    }
    printf("\n");
    return 0;
}
```

## 函数

```c
#include <stdio.h>

int power(int base, int n)
{
    int i, p;
    p = 1;
    for (i = 1; i <= n; i++) {
        p *= base;
    }
    return p;
}

int main(int argc, const char * argv[]) {
    int i;
    for (i = 0; i < 31; i++) {
        printf("%d %d\n", i, power(2, i));
    }
    return 0;
}
```

输出结果：

```c
 0 1
 1 2
 2 4
 3 8
 4 16
 5 32
 6 64
 7 128
 8 256
 9 512
10 1024
...
30 1073741824
```




