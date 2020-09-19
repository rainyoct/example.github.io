---
layout: post
title: 块设备文件系统与开放通道闪存
category: technology
tags: File System
description: overview
---

# 本篇总结主要包括VFS读写流程、块I/O机制、Open-channel SSD (主要为LightNVM)、块设备文件系统(主要为Btrfs及F2FS)

## VFS I/O Stack

[Linux VFS机制简析](https://www.cnblogs.com/jimbo17/archive/2004/01/13/10107318.html)

## VFS与具体文件系统的配合 (page cache / write back 等等)

[Linux Kernel文件系统写I/O流程代码分析](https://www.cnblogs.com/jimbo17/archive/2004/01/13/10436222.html)

[bio 与块设备驱动](https://blog.csdn.net/jemmy858585/article/details/43937149)

[Linux块设备IO子系统](https://www.cnblogs.com/xiaojiang1025/p/6500557.html)

make_request_fn钩子函数有VFS默认的，也可以由设备挂载时设置

[浅谈Linux内核IO体系之磁盘IO](https://zhuanlan.zhihu.com/p/96391501)

## LightNVM

[FAST'17](https://www.usenix.org/conference/fast17/technical-sessions/presentation/bjorling)

[LightNVM简介](https://blog.xiocs.com/archives/9/)

## 

[IBM](https://www.ibm.com/developerworks/cn/linux/l-jffs2/)

## UBIFS

[概述](https://www.cnblogs.com/embedded-linux/p/6241817.html)

[ubifs- Wandering Tree](https://blog.csdn.net/fervor_heart/article/details/8908868)

## LogFS

论文：LogFS - finally a scalable flash file system

## 对比

[ChinaUnix](http://blog.chinaunix.net/uid-23381466-id-3411483.html)

[Cramfs JFFS2 YAFFS2](https://blog.csdn.net/daofengdeba/article/details/7721340)