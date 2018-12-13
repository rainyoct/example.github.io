---
layout: post
title: Parallel Trees
category: brick
tags: 搬砖
keywords: 论文
---

## B+Tree

The Performance of Current B-Tree Algorithms

本文有各式传统B+Tree并行锁算法

## B-link Tree

Efficient Locking for Concurrent Operations on B-Trees

## NV-Tree

NV-Tree: A Consistent and Workload-Adaptive Tree Structure for Non-Volatile Memory

## FP-Tree

硬件粗粒度并行

## PALM-Tree

BSP模型


## Lock-free  
主要知识点：
* CAS, DwCAS, LL/SC 等primitive
* ABA问题
* 内存模型

[What is lock free](http://www.cnblogs.com/gaochundong/p/lock_free_programming.html)  
[无锁数据结构](http://blog.jobbole.com/90811/)  

lock-free就是指线程相互之间不干扰，不会因为别的线程出问题而自己陷入死循环。  
因此，设计lock-free主要注意两点：  
* 遇到困境别傻等，不断往满足条件的方向去努力，把路走活
* 做事留一线，共享的东西不要了留个中间态，等大家都不要了再去真正扔掉