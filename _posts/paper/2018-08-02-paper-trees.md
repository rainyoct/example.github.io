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
* ABA问题 (采用DCAS同步更新版本号等额外信息得以解决)
* 内存模型
* 一些基本的lock-free数据结构
* [DCAS也并不是silver bullet](http://people.csail.mit.edu/shanir/publications/DCAS.pdf)  (废话，这世界哪有silver bullet)
* [就连lock-free自己也不是](http://www.cs.umd.edu/~abadi/papers/latch-free-cidr2017.pdf)


[What is lock free](http://www.cnblogs.com/gaochundong/p/lock_free_programming.html)  
[无锁数据结构](http://blog.jobbole.com/90811/)  


Bw-Tree采用CSA加上复杂的算法实现lock-free，而[Bz-Tree](https://dl.acm.org/doi/abs/10.1145/3164135.3164147)采用[PMwCAS](https://ieeexplore.ieee.org/abstract/document/8509270)实现更高效的并发，[论文讲解1](http://sel-fish.net/2018/10/24/pmwcas/)，[论文讲解2](https://zhuanlan.zhihu.com/p/43390204)


PMwCAS的并发算法源于[多字CAS算法](https://zhuanlan.zhihu.com/p/103989987)，[A Practical Multi-Word Compare-and-Swap Operation](https://www.cl.cam.ac.uk/research/srg/netos/papers/2002-casn.pdf)

基本思路是保证各线程按照相同的顺序访问word，从而确保未被标记的word一定是干净且可被修改的。每个线程先从自己想改的第一个word开始标记指针，指向自己申请好的描述符，如果被别人标记过了，就先帮别人完成工作(根据别人申请的描述符里面的内容)。然后再从第一个word开始向后更新，不用害怕别人把自己标记的更新了，因为其他线程遇见后会协助自己的更新操作。由于各线程方向一致，互相帮助，所以不会存在死锁，也不会因为一个线程挂掉而陷入死循环。


lock-free就是指线程相互之间不干扰，不会因为别的线程出问题而自己陷入死循环。
因此，设计lock-free主要注意两点：  
* 遇到困境别傻等，不断往满足条件的方向去努力，把路走活
* 做事留一线，共享的东西不要了留个中间态，等大家都不要了再去真正扔掉