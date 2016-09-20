---
title: Ubuntu日记01-修复模式
tag: [ ubuntu, recovery, passwd]
category: Ubuntu日记
date: 2016-06-24
---

# 使用ubuntu修复模式
**2016.4.5 重庆 阴**

今天使用ubuntu时遇到了一种启动不了的情况，因为自己根据网上的教程修改了/etc/modules文件，然而启动式发生错误，导致不能启动。 因为自己原来遇到过忘记密码进不去的情况，所以大致知道怎么解决。

1. 在grub启动中选择advanced options -> recovery mode (don't press 'enter' key!) -> press 'e' key enter edit mode.
2. 修改其中的"ro recovery nomodeset"为"rw single init=/bin/bash", then press 'ctrl+X' and you will get a bash shell as root.
3. 如果你想要修改自己的密码直接使用 passwd 命令

参考：[http://taobao3ef.blog.163.com/](http://taobao3ef.blog.163.com/)
