---
layout: post
title: Memory Bank Conflict
category: technology
tags: Memory Bank
description: Memory Bank
---

[What is memory bank?](https://blog.csdn.net/m0_37561165/article/details/81704977)  

Why conflict?  
一个bank的地址解码器只有一个，如果多个线程访问同一个bank，就只能顺序操作。  

How to mitigate it?  
由于DRAM的物理地址是系统管理的，从程序员的视角来说，无法通过对虚拟地址的操作来避免硬件的conflict。  
且物理地址本身也会通过[memory controller](https://blog.csdn.net/thisway_diy/article/details/79389530)映射到真实的存储单元上（算法也是保密的），因此，即便通过内核找到物理地址，也无法确保避免conflict。  

## 但是，CUDA中的shared memory是由程序直接访问的,与寄存器同级。
[CUDA并行存储模型](https://www.cnblogs.com/liangliangdetianxia/p/3991042.html)
