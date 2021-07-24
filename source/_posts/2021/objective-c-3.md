---
title: 《Objective-C高级编程》学习笔记（3）
categories:
  - Objective-C
tags:
  - Objective-C
date: 2021-03-01 21:21:51
---

《Objective-C高级编程》学习笔记。GCD。

<!-- more -->

GCD全称 Grand Central Dispatch。GCD是异步执行任务的技术之一。

### 多线程编程

多线程更新相同的资源会导致数据不一致，会造成死锁，使用太多线程会消耗大量内存。

使用线程，不妨碍主循环的执行。

#### Dispatch Queue

Serial Dispatch Queue: 使用一个线程串行执行。

Concurrent Dispatch Queue：使用多个线程并行执行，取决于当前系统的状态。 

Main Dispatch Queue: 主线程。

Global Dispatch Queue：一种系统提供的Concurrent Dispatch Queue，包含4各执行优先级。

dispatch_set_traget_queue 变更执行优先级。

dispatch_after 可以作为粗略的闹钟功能使用。

dispatch_group。

dispatch_barrier_async：配合Concurrent Dispatch Queue一起使用可实现高效的数据库访问和文件访问。

dispatch_sync: 容易引起死锁。

dispatch_apply:该函数按指定的次数将指定的Block追加到指定的queue中，并等待全部处理执行结束。

dispatch_semaphore:可进行更细粒度的排他控制。

dispatch_once: 只执行一次，在多线程下也能保证安全。

Dispatch I/O: 可提高文件的读取速度。

上面是GCD的一些常用API，使用这些api可以方便的实现多线程。

