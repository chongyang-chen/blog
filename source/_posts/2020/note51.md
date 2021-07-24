---
title: 数据结构学习笔记（二）
categories:
  - data struct
tags:
  - 数据结构
date: 2018-07-31 19:11:06
---

C语言基础
在前面自己重新学习了C语言，对C语言掌握了大概。今天重新回顾一下C语言的基础知识。
<!-- more -->
C语言开发环境
macOC下使用Xcode开发。
递归与非递归
函数的递归就是自己调用自己，可以是直接调用自己，也可以是间接调用自己。利用递归求阶乘（规定：0！= 1），求斐波那契数列，解决汉诺塔问题。
任何能用递归解决的问题都能用迭代的方法解决，简单的递归可以用迭代转化为非递归，复杂的递归问题，需要用数据结构中的栈来消除递归。

```C
// 阶乘
long factorial(int n){
    if (n == 0){
        return 1;
    } else {
        return (n * factorial(n - 1));
    }
}

//发现n个数中的最大的那个数
int findmax(int a[], int n){
    int m;
    if(n <= 1){
        return a[0];
    } else {
        m = findmax(a, n-1);
        return a[n-1] >= m ? a[n-1] : m;
    }
}

//正整数n的不增的和式分解结果
void rd(int a[], int i, int k){
    int j, p;
    for (j = i; j >= 1; j--){
        if (j <= a[k-1]){
            a[k] = j;
            if(j == i){
                printf("%d = %d", a[0], a[1]);
                for (p = 2; p <= k; p++) {
                    printf("+%d", a[p]);
                }
                printf("\n");
            } else {
                rd(a, i-j, k+1);
            }
        }
    }
    
}

//大整数阶乘
void fact(int a[], int k){
    int *b, m, i, j, r, carry;
    m = a[0];
    b = (int *)malloc(sizeof(int) * (m+1));
    for (int i = 1; i <= m; i++) {
        b[i] = a[i];
    }
    for (j = 1; j < k; j++){
        for(carry = 0, i = 1; i <= m; i++){
            r = (i<=a[0]?a[i] + b[i]:a[i]) + carry;
            a[i] = r % 10;
            carry = r / 10;
        }
        if (carry){
            a[++m] = carry;
        }
    }
    free(b);
    a[0] = m;
}

void writefact(int *a, int k){
    int i;
    //printf("%4d!的阶乘有%d位\n",k ,a[0]);//2018!的阶乘有5795位,末尾502个零
    printf("%4d! = ", k);
    
    for (i = a[0]; i > 0; i--) {
        printf("%d", a[i]);
    }
    printf("\n");
}

int main(int argc, const char * argv[]) {
    // insert code here...
#if 0
    printf("Hello, World!\n");
    int num;
    for(num = 0; num < 1; num++){
        printf("%d! = %ld\n", num, factorial(num));
    }
    
    int a[N], n, i;
    printf("请输入n的值：");
    scanf("%d", &n);
    printf("请依次输入%d个数：\n", n);
    for (i = 0; i < n; i++) {
        scanf("%d", &a[i]);
    }
    printf("在这%d个数中，最大的元素是%d\n", n, findmax(a, n));
#endif
    
#if 0
    int n, a[N];
    printf("请输入一个正整数n（n < 20）:");
    scanf("%d", &n);
    a[0] = n;
    printf("不增的和式分解结果：\n");
    rd(a, n, 1);
    
#endif
    
    int a[N], n, k;
    printf("请输入n的值：");
    scanf("%d", &n);
    a[0] = 1;
    a[1] = 1;
    writefact(a, 1);
    for (k = 2; k <= n; k++){
        fact(a, k);
        writefact(a, k);
    }
    
    return 0;
}
```

