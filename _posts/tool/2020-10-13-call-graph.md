---
layout: post
title: Call Graph
category: tool
tags: 工具
description: Graphviz + CodeViz
---

### Graphviz + CodeViz

网上有很多安装教程

[看开源代码利器—用Graphviz + CodeViz生成C/C++函数调用图(call graph)](https://www.cnblogs.com/lanxuezaipiao/p/3450201.html)

主要有几个地方值得注意：

1. CodeViz自带gcc安装脚本，并指定了对应的版本。然而，脚本中的下载链接可能无法连通。因此，需要手动下载对应版本的gcc源码并放在compilers目录。此时可能提示有一些依赖包（GMP、MPFR、MPC这三个库）不存在，需要进入compilers目录下的/gcc-graph/gcc-4.6.2/contrib/目录，使用download_prerequisites脚本自动下载。注意，一定要先把这个脚本cp到父目录gcc源码下再执行，这样下载的依赖包才能被compiler调用到。

2. 可能会出现fatal error: bits/libc-header-start.h: No such file or directory等错误，这些都是编译gcc过程中产生的问题，需要sudo apt-get install gcc-multilib等方法补足编译环境。

3. 编译老版本的gcc源码可能出现不兼容的类型名，需要手动修改一下源码。如：compilers/gcc-graph/gcc-4.6.2/gcc/config/i386/linux-unwind.h中的struct siginfo 需要修改为 struct siginfo_t（注意要把compiler install脚本中的解压命令给注释掉，不然白改了）。

4. gcc编译还可能遇到[一些其他的问题](https://www.jianshu.com/p/b3ed2b3652ac)，非常复杂。

### 最后还是通过doxygen替代了CodeViz，大概这就是人生吧

[Linux安装](https://www.cnblogs.com/274914765qq/p/4443328.html)（配置参数较老，需要参考Windows的选项手动配置）

[Windows安装及配置](https://blog.csdn.net/benkaoya/article/details/79763668)