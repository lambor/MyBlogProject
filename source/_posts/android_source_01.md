---
title: Android源码分析01-源码编译
tag: [ android, source, build]
category: Android源码
---

#  源码编译

买了《Android源码情景分析》，于是就照着书上过一遍源码，熟悉一下底层。

##  环境

摘自[自己动手编译Android源码(超详细](http://www.jianshu.com/p/367f0886e62b),关于最新环境配置，详情见该文章。

| Android版本 | 编译要求的Ubuntu最低版本 |
|-|-|
| Android 6.0至AOSP master  |   Ubuntu 14.04 |
| Android 2.3.x至Android 5.x |   Ubuntu 12.04 |
| Android 1.5至Android 2.2.x |   Ubuntu 10.04 |

| Android版本 | 编译要求的JDK版本 |
|-|-|
| AOSP的Android主线                   | OpenJDK 8    |
| Android 5.x至android 6.0         | OpenJDK 7    |
| Android 2.3.x至Android 4.4.x | Oracle JDK 6  |
| Android 1.5至Android 2.2.x     | Oracle JDK 5  |

### 安装虚拟机

书中使用的是android2.3.1_r1，所以我使用的是ubuntu12.04-desktop(server版本好像不能安装增强模块，不能使用共享文件夹),java版本为oracle jdk 6。
因为我在ubuntu15.10下工作，所以使用virtualbox虚拟机(在ubuntu15.10下编译会报make错误)。
使用虚拟机时，使用USB和共享文件夹功能需要安装增强模块。
推荐使用共享文件夹，因为USB在编译时遇到execute权限问题,解决起来很麻烦。
在进入共享文件夹时，会遇到权限问题，这时只需要

```
$ sudo usermod +a +G vboxsf <USERNAME>
$ groups <USERNAME>
```

### 安装依赖

根据[官网](https://source.android.com/source/initializing.html)的提示安装ubuntu12.04依赖时，
```
$ sudo apt-get install git gnupg flex bison gperf build-essential \
  zip curl libc6-dev libncurses5-dev:i386 x11proto-core-dev \
  libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-glx:i386 \
  libgl1-mesa-dev g++-multilib mingw32 tofrodos \
  python-markdown libxml2-utils xsltproc zlib1g-dev:i386
$ sudo ln -s /usr/lib/i386-linux-gnu/mesa/libGL.so.1 /usr/lib/i386-linux-gnu/libGL.so
```
会出现重启虚拟机后不能进入GUI桌面。

解决方法是[http://stackoverflow.com/questions/23254439/android-setting-up-a-linux-build-environment-libgl1-mesa-glxi386-package-have](http://stackoverflow.com/questions/23254439/android-setting-up-a-linux-build-environment-libgl1-mesa-glxi386-package-have)

然而我是在**安装依赖之前**直接将启动模式改为命令行模式。

```
$ sudo nano /etc/default/grub
- GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
+ GRUB_CMDLINE_LINUX_DEFAULT="text"
$ sudo update-grub
```

### 安装Oracle Java

```
$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java6-installer
```

## 编译

```
$ source build/envsetup.sh
$ lunch
$ make
$ emulator
```

### 编译遇到的问题

编译过程中会遇到ln创建symbolic link错误，报错原因为read-only filesystem。
是因为VirtualBox使用的share folder。解决方法：
```
$ VBoxManage setextradata android12.04 VBoxInternal2/SharedFoldersEnableSymlinksCreate/android_base 1
```

### 运行时遇到的问题

由于我是直接make，而不是lunch，所以没有emulator的使用环境。于是需要通过
命令行来设置环境 `emulator_env_set.sh`
```
#!/bin/bash
set PWD="`pwd`"
PATH=$PATH:$PWD/out/host/linux-x86/bin
export ANDROID_PRODUCT_OUT=$PWD/out/target/product/generic
```

```
$ sudo chmod +x ./emulator_env_set.sh
$ source ./emulator_env_set.sh
$ emulator
```

由于我是在宿主机中运行emulator，而在虚拟机中编译（我的虚拟机是命令行，不能运行）,
所以没有相应的运行环境，所以会报错 SDL init failure, reason is: No available video device
解决方法：http://stackoverflow.com/questions/4841908/sdl-init-failure-reason-is-no-available-video-device

```
sudo apt-get install libsdl1.2debian:i386
```

## 最后
最终显示出android的界面