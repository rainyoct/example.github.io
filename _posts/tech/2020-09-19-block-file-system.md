---
layout: post
title: 块设备文件系统与开放通道闪存
category: technology
tags: File System
description: overview
---

# 本篇总结主要包括VFS读写流程、块I/O机制、Open-channel SSD (主要为LightNVM)、块设备文件系统(主要为Btrfs)

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

## Btrfs

[TOS](https://dl.acm.org/doi/abs/10.1145/2501620.2501623)

Btrfs使用extent节点来减少分配开销，但与Ext4不同的是，Btrfs整个文件系统的布局为一棵B-Tree。因此，其具有更好的扩展性，如inode数量不受限(因为无需存放在固定的superblock中)，且扩容更加方便（无需重新布局元数据）等。

Ext4采用Journaling的方式维持数据一致性，而Btrfs采用COW的方式，即overwrite操作会把数据页写在新的页上，旧页作废，同时修改父节点的相应指针。对于extent节点来说，由于COW的新页与旧的extent不再连惯，还存在着节点分裂的开销。而父节点的修改同样需要采用COW机制，这就使得对数据页的一次overwrite实际会被传播到root，即wandering tree问题。