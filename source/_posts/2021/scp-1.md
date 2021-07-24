---
title: 如何将一个服务器上的文件或者文件夹复制到另一台服务器上
categories:
  - linux
tags:
  - scp
  - linux
date: 2021-03-05 17:41:49
---

要实现题目描述的功能，可以使用 scp 命令。

<!-- more -->

### 将本地文件夹拷贝到远程

scp -r 目录名 用户名@计算机IP或者计算机名称:远程路径

`scp -r /home/test1 zhidao@192.168.0.1:/home/test2`

test1为源目录，test2为目标目录，zhidao@192.168.0.1为远程服务器的用户名和ip地址。

详细的 scp 命令可以查看下面的地址：

[Linux scp命令](https://www.runoob.com/linux/linux-comm-scp.html)

