---
title: 周记总结01-2016.10.22
tag: [ week_note, linux, android ]
category: 周记总结
date: 2016-10-22
---

#  第1周总结

为了总结一周学习的零碎知识,于是开了这个系列,希望能够每周总结一下坚持下去。

##  Linux

### 对Pipe的理解 

原来对pipe的理解有误解,我以为pipe两边的进程是串行执行的,但读过<Unix/Linux编程实践教程>,发现原来是并行运行的.

通过实验验证: `strace -f bash -c 'ls | grep hello'`2>&1 | grep --color -E 'exe|pip|$'`

> `strace -f`     follow forks
> `bash -c`       commands are read from the first non-option argument command_string
> `grep -E "$"`   every line is grepped

查看输出即可发现`ls`和`grep`是同时fork出来的．

而且发现是先pip的`pipe([3,4])`，为什么是`pipe([3,4])`而不是`pipe([1,2])`呢?

因为`bash -c "command"`也是从当前bash fork出来的,所以1,2为当前bash的stdin和stdout.

### 关于PATH的文件位置

> ~/.profile 加载于login shell
> ~/.bashrc  加载于interactive terminal
> ~/.pam_enviroment GUI launcher点击启动加载

### 关于应用安装包解压安装位置

unix 推荐`/opt/` 不会被系统升级覆盖
旧的位置`/usr/local/bin`

### 挂载网络文件系统

最近有用虚拟机，没有使用虚拟机提供的共享文件夹功能，而是尝试了一下nfs(network file system)

首先要在服务端（提供共享）安装nfs,并配置
```
$ apt-get install nfs-kernele-server
$ apt-get install nfs-common
$ echo "<share directory path> <allow ips>(rw,sync,no_root_squash)" >> /etc/exports
```
然后在客户端安装
```
$ apt-get install nfs-common
$ mount -t nfs <server ip>:<server share directory path> <local mount point>
```

### set和stty

对于bash built-in command是不能用man来查询的，需要使用help,例如`help set`.并且help也是built-in command

stty是设置tty输入输出等相关属性的
set是设置shell的一些属性和环境变量的

## Android

### Toast

Toast 不需要在 UI线程中显示,只需要有Looper环境的线程就行

### Service & AIDL
虽然`onStartCommand`中的操作是线程同步的,好象是在UI线程中
但是对于使用AIDL中的服务操作,却不是线程同步的.


