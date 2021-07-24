---
title: 学习笔记之C语言（2）
date: 2010-11-09 19:49:05
categories:
- C语言
tags:
- C语言
---

## 数据类型及长度

```c
Size of char 8
Size of char max 127
Size of char min -128
Size of unsigned char 255
Size of short min -32768
Size of short max 32767
Size of unsigned short 65535
Size of int min -2147483648
Size of int max 2147483647
Size of unsigned int 4294967295
Size of long min -9223372036854775808
Size of long max 9223372036854775807
Size of unsigned long 18446744073709551615
Size of long long min -9223372036854775808
Size of long long max 9223372036854775807
Size of unsigned long long 18446744073709551615
```

<!-- more -->

## 算数运算符

```c
int year = 2020;
if ((year % 4 == 0 && year % 100 != 0) || year % 400 == 0)
    printf("%d is a leap year\n", year);
else
    printf("%d is not a leap year\n", year);
```

2020年是闰年。

## 关系运算符与逻辑运算符

关系运算符包括：>, >=, <, <=, ==, !=。关系运算符优先级比算数运算符低。  
逻辑运算符 && 与 || ，在知道结果后立即停止计算。

## 类型转换

```c
int a2i(char s[]) {
    int i, n;
    n = 0;
    for (i = 0; s[i] >= '0' && s[i] <= '9'; i++) {
        n = n * 10 + (s[i] - '0');
    }
    return n;
}
```

16进制转10进制：

```c
int hexalpha_to_int(int c) {
    char hexalpha[] = "aAbBcCdDeEfF";
    int i;
    int answer = 0;
    for(i = 0; hexalpha[i] != '\0'; i++) {
        if(hexalpha[i] == c) {
            answer = 10 + (i / 2); }
    }
    return answer;
}

unsigned int htoi(const char s[]) {
    unsigned int answer = 0;
    int i = 0;
    int valid = 1;
    int hexit;
    if(s[i] == '0') {
        ++i;
        if(s[i] == 'x' || s[i] == 'X') {
            ++i;
        }
    }
    while(valid && s[i] != '\0') {
        answer = answer * 16;
        if(s[i] >= '0' && s[i] <= '9') {
            answer = answer + (s[i] - '0');
        }
        else
        {
            hexit = hexalpha_to_int(s[i]);
            if(hexit == 0)
            {
                valid = 0;
            }
            else
            {
                answer = answer + hexit;
            }
        }
        ++i;
    }
    if(!valid) {
        answer = 0;
    }
    return answer;
}
```

## 自增运算符与自减运算符

如果n的值是5，那么 `x = n++;`x的值为5，而`x = ++n;`x的值为6。
在仅需要递增变量的情况下，两种方式的效果相同。

## 位运算符

```c
unsigned getbits(unsigned x, int p, int n){
    return (x >> (p+1-n)) & ~(~0 << n);
}
```

练习2-6，2-7，2-8。

```c
unsigned setbits(unsigned x, int p, int n, unsigned y) {
    return (x & ((~0 << (p + 1)) | (~(~0 << (p + 1 - n))))) | ((y & ~(~0 << n)) << (p + 1 - n));
}

unsigned invert(unsigned x, int p, int n) {
    return x ^ (~(~0U << n) << p); 
}

unsigned rightrot(unsigned x, unsigned n) {
    while (n > 0) {
        if ((x & 1) == 1)
            x = (x >> 1) | ~(~0U >> 1);
        else
            x = (x >> 1); 
        n--;
    }
    return x;
}
```

## 赋值运算符

```c
int bitcount1(unsigned x)
{
    int b;
    for (b = 0; x != 0; x >>= 1)
        if (x & 01)
            b++;
    return b;
}

int bitcount2(unsigned x)
{
    int b;
    for (b = 0; x != 0; x &= (x-1))
        b++;
    return b;
}
```

计算整数二进制中1的个数。

表达式 `x &= (x – 1)`可以删除 x 中最右边值为 1 的 一个二进制位。

## 运算符优先级

算数运算符优先级大于比较运算符，&&优先级大于||。





