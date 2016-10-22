---
title: Android源码分析03-goldfish内核编译
tag: [ android, source, build, kernel, goldfish ]
category: Android源码
date: 2016-08-22
---

#  goldfish内核编译

第三章有需要用到android内核源码.

### 环境

关于android内核版本与发行版本对应关系,[这篇文章](http://www.cnblogs.com/qiengo/archive/2012/07/16/2593234.html)有详细的记录

对于本次使用的android2.3.1_r1对应关系如下

| 英文名 | 中文名 | 版本号 | API Level | 发布时间 | 内核版本 |
|-|-|-|-|-|-|
| Gingerbread | 姜饼 | 2.3-2.3.2 | 9,NDK5 | 2010,12 | 2.6.35 |


