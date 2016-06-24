---
title: Ubuntu日记02-WIFI hotspot
tag: [ ubuntu, wifi, hotspot]
category: Ubuntu日记
---

# ubuntu 15.10 wifi hotspot
**2016.4.6 重庆 阴**

我想说的是在ubuntu上开wifi热点真是麻烦。原来有ap-hotspot，然后就去查了一下发现已停止更新了，并且15.10的没有安装源。然后我就找到了他推荐的create_ap.

安装倒是很简单，但是使用时会报错，表示没有找到hostapd，然后在工程的howto路径找到了解决方法。（注意：命令行有一定出入，因为使用的时gitclone所以可能有版本更新，所以把命令中的版本号改成相应的就行了）然后在make时报错：fatal error: netlink/genl/genl.h: No such file or directory.然后找到了相应解决方法.然后就运行create_ap wlxe84e062010e1 enp3s0 ahaha 789456123 就行了。

总结，自己真能折腾。折腾中发现了apt-file这个工具，可以寻找缺失的dependecies.
