---
layout: post
title: MySQL引擎的锁机制
category: technology
tags: MySQL
description: overview
---

## InnoDB

[CSDN](https://blog.csdn.net/yuanrxdu/article/details/41170381)

## MyISAM

[MyISAM](https://www.2cto.com/database/201508/429974.html)

[并发控制 mysql MyISAM表锁](https://www.cnblogs.com/qq78292959/archive/2013/01/30/2883109.html)

概述:<br>
相对其他数据库而言，MySQL的锁机制比较简单，其最显著的特点是不同的存储引擎支持不同的锁机制。<br>
``MyISAM``和``MEMORY``存储引擎采用的是表级锁（table-level locking）；<br>
``BDB``存储引擎采用的是页面锁（page-level locking），但也支持表级锁；<br>
``InnoDB``存储引擎既支持行级锁（row-level locking），也支持表级锁，但默认情况下是采用行级锁。<br>
MySQL这3种锁的特性可大致归纳如下。<br>
    "+" 表级锁：开销小，加锁快；不会出现死锁；锁定粒度大，发生锁冲突的概率最高,并发度最低。  
    "+" 行级锁：开销大，加锁慢；会出现死锁；锁定粒度最小，发生锁冲突的概率最低,并发度也最高。  
    "+" 页面锁：开销和加锁时间界于表锁和行锁之间；会出现死锁；锁定粒度界于表锁和行锁之间，并发度一般。  