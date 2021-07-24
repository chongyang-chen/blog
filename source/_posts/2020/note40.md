---
title: Socket编程
date: 2018-01-05 19:34:36
tags:
- C
- socket
categories:
- C
---

### TCP的套接字的socket编程：

服务器端程序流程：

1. 创建套接字socket。
2. 将创建的套接字绑定（bind）到本地的地址和端口上。
3. 设置套接字的状态为监听状态（listen），准备接受客户端的连接请求。
4. 接受请求（accpet），同时返回得到一个用户连接的新套接字。
5. 使用这个新套接字进行通信（send/recv）。
6. 通信完毕，释放套接字资源。

客户端程序：

1. 创建套接字。
2. 向服务器发出连接请求（connect）。
3. 请求连接后与服务器进行通信操作。
4. 释放套接字资源。

### UDP的套接字的socket编程：

服务器端程序流程：

1. 创建套接字socket。
2. 将创建的套接字绑定（bind）到本地的地址和端口上。
3. 等待接收数据。
4. 释放套接字资源。

客户端程序：

1. 创建套接字。
2. 向服务器发送数据。
4. 释放套接字资源。

<!-- more -->

### 基于tcp的socket连接

首先创建tcp服务器端。

```C
//
//  main.c
//  socketc
//
//  Created by ccyag on 9/1/18.
//  Copyright © 2018年 ccyag. All rights reserved.
//

/*socket tcp服务器端*/
#include <sys/stat.h>
#include <fcntl.h>
#include <errno.h>
#include <netdb.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>

#define SERVER_PORT 5555

/*
 监听后，一直处于accept阻塞状态，
 直到有客户端连接，
 当客户端如数quit后，断开与客户端的连接
 */

int main()
{
    //调用socket函数返回的文件描述符
    int serverSocket;
    //声明两个套接字sockaddr_in结构体变量，分别表示客户端和服务器
    struct sockaddr_in server_addr;
    struct sockaddr_in clientAddr;
    int addr_len = sizeof(clientAddr);
    int client;
    char buffer[200];
    int iDataNum;
    
    //socket函数，失败返回-1
    //int socket(int domain, int type, int protocol);
    //第一个参数表示使用的地址类型，一般都是ipv4，AF_INET
    //第二个参数表示套接字类型：tcp：面向连接的稳定数据传输SOCK_STREAM
    //第三个参数设置为0
    if((serverSocket = socket(AF_INET, SOCK_STREAM, 0)) < 0)
    {
        perror("socket");
        return 1;
    }
    
    bzero(&server_addr, sizeof(server_addr));
    //初始化服务器端的套接字，并用htons和htonl将端口和地址转成网络字节序
    server_addr.sin_family = AF_INET;
    server_addr.sin_port = htons(SERVER_PORT);
    //ip可是是本服务器的ip，也可以用宏INADDR_ANY代替，代表0.0.0.0，表明所有地址
    server_addr.sin_addr.s_addr = htonl(INADDR_ANY);
    //对于bind，accept之类的函数，里面套接字参数都是需要强制转换成(struct sockaddr *)
    //bind三个参数：服务器端的套接字的文件描述符，
    if(bind(serverSocket, (struct sockaddr *)&server_addr, sizeof(server_addr)) < 0)
    {
        perror("connect");
        return 1;
    }
    //设置服务器上的socket为监听状态
    if(listen(serverSocket, 5) < 0)
    {
        perror("listen");
        return 1;
    }
    
    while(1)
    {
        printf("Listening on port: %d\n", SERVER_PORT);
        //调用accept函数后，会进入阻塞状态
        //accept返回一个套接字的文件描述符，这样服务器端便有两个套接字的文件描述符，
        //serverSocket和client。
        //serverSocket仍然继续在监听状态，client则负责接收和发送数据
        //clientAddr是一个传出参数，accept返回时，传出客户端的地址和端口号
        //addr_len是一个传入-传出参数，传入的是调用者提供的缓冲区的clientAddr的长度，以避免缓冲区溢出。
        //传出的是客户端地址结构体的实际长度。
        //出错返回-1
        client = accept(serverSocket, (struct sockaddr*)&clientAddr, (socklen_t*)&addr_len);
        if(client < 0)
        {
            perror("accept");
            continue;
        }
        printf("\nrecv client data...n");
        //inet_ntoa   ip地址转换函数，将网络字节序IP转换为点分十进制IP
        //表达式：char *inet_ntoa (struct in_addr);
        printf("IP is %s\n", inet_ntoa(clientAddr.sin_addr));
        printf("Port is %d\n", htons(clientAddr.sin_port));
        while(1)
        {
            iDataNum = recv(client, buffer, 1024, 0);
            if(iDataNum < 0)
            {
                perror("recv");
                continue;
            }
            buffer[iDataNum] = '\0';
            if(strcmp(buffer, "quit") == 0)
                break;
            printf("%drecv data is %s\n", iDataNum, buffer);
            send(client, buffer, iDataNum, 0);
        }
    }
    return 0;
}  

```

然后创建客户端程序：

```C
//
//  main.c
//  client
//
//  Created by ccyag on 9/1/18.
//  Copyright © 2018年 ccyag. All rights reserved.
//

/*socket tcp客户端*/
#include <sys/stat.h>
#include <fcntl.h>
#include <errno.h>
#include <netdb.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <unistd.h>

#define SERVER_PORT 5555

/*
 连接到服务器后，会不停循环，等待输入，
 输入quit后，断开与服务器的连接
 */

int main()
{
    //客户端只需要一个套接字文件描述符，用于和服务器通信
    int clientSocket;
    //描述服务器的socket
    struct sockaddr_in serverAddr;
    char sendbuf[200];
    char recvbuf[200];
    int iDataNum;
    if((clientSocket = socket(AF_INET, SOCK_STREAM, 0)) < 0)
    {
        perror("socket");
        return 1;
    }
    
    serverAddr.sin_family = AF_INET;
    serverAddr.sin_port = htons(SERVER_PORT);
    //指定服务器端的ip，本地测试：127.0.0.1
    //inet_addr()函数，将点分十进制IP转换成网络字节序IP
    serverAddr.sin_addr.s_addr = inet_addr("127.0.0.1");
    if(connect(clientSocket, (struct sockaddr *)&serverAddr, sizeof(serverAddr)) < 0)
    {
        perror("connect");
        return 1;
    }
    
    printf("connect with destination host...\n");
    
    while(1)
    {
        printf("Input your world:>");
        scanf("%s", sendbuf);
        printf("\n");
        
        send(clientSocket, sendbuf, strlen(sendbuf), 0);
        if(strcmp(sendbuf, "quit") == 0)
            break;
        iDataNum = recv(clientSocket, recvbuf, 200, 0);
        recvbuf[iDataNum] = '\0';
        printf("recv data of my world is: %s\n", recvbuf);
    }
    close(clientSocket);
    return 0;
}  


```
先运行服务器端程序，再运行客户端程序，在客户端输入内容，服务器端可以收到发送的内容。

