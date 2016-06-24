---
title: Ubuntu日记03-APT Log
tag: [ ubuntu, apt, log]
category: Ubuntu日记
---

# 关于APT Log
**2016.4.6 晚 重庆 阴**

下午干了一件很刺激的事：apt-get autoremove
一下将很多的软件包给删了。当时就觉得不对，于是上网一搜吓得我一身冷汗。

因为重启后发现自己的网络管理也打不开了，更别说用VPN去google，这时候我想到了BING,搜到了怎么找到apt操作的历史：http://ubuntuforums.org/showthread.php?t=2258741

于是自己写了一个简单的python脚本，用来将历史中的autoremove包名总结出来。最后再apt-get install.

```python
#从history.log中找到的当时autoremove卸载的包，内容省略
packages = "libqt5script5:amd64 (5.4.2+dfsg-4), libkf5completion5:amd64 (5.15.0-0ubuntu1), kpackagelauncherqml:amd64 (5.15.0-0ubuntu1), libfam0:amd64 (2.7.0-17.1)..."

final_string = ""
for package in packages.split(","):
    final_string += package.split(":")[0]
print final_string
```
