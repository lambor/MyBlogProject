---
title: Android源码分析02-goldfish内核编译
tag: [ android, source, build, kernel, goldfish ]
category: Android源码
date: 2016-10-15
---

#  goldfish内核编译

第三章有需要用到android内核源码.

### 环境

关于android内核版本与发行版本对应关系,[这篇文章](http://www.cnblogs.com/qiengo/archive/2012/07/16/2593234.html)有详细的记录

对于本次使用的android2.3.1_r1对应关系如下

| 英文名 | 中文名 | 版本号 | API Level | 发布时间 | 内核版本 |
|-|-|-|-|-|-|
| Gingerbread | 姜饼 | 2.3-2.3.2 | 9,NDK5 | 2010,12 | 2.6.35 |

但是为了和老罗的保持一致,所以最后选择了稍旧版本 2.6.29

下载goldfish源码
```
$ mkdir android_kernal
$ cd android_kernal
$ git clone http://android.googlesource.com/kernel/goldfish.git
$ cd <the source dir>
$ git branch -a
$ git checkout <the version you want branch>
```
注意,我们需要的是适用于模拟器用的内核,所以需要checkout archive版本

### 编译

goldfish下载好后,就开始编译

##### 准备

首先将位于Android源码(不是goldfish源码)中的交叉编译工具路径添加到PATH环境中
```
$ export PATH=$PATH:<root dir of android src>/prebuilt/linux-x86/toolchain/arm-eabi-4.4.3/bin
```

然后修改goldfish源码的Makefile文件
```
- ARCH          ?= $(SUBARCH)
- CROSS_COMPILE ?=
+ ARCH          ?= arm
+ CROSS_COMPILE ?= arm-eabi-
```
也可以不删除,注释掉那两行就行了.

##### 开始编译

```
$ cd goldfish
$ make goldfish_defconfig
$ make
```

编译成功后,会看到最后输出
```
OBJCOPY arch/arm/boot/zImage
Kernel: arch/arm/boot/zImage is ready
```

### 运行

启动模拟器,并指定kernel
```
$ emulator -kernel <generated kernel image file path> 
```

使用adb查看内核版本信息
```
$ adb shell
$$ cd proc
$$ cat version 
```
发现模拟器使用的内核及刚刚编译的.

### 参考

[老罗的文章](http://blog.csdn.net/luoshengyang/article/details/6564592)


