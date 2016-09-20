---
title: Ubuntu日记04-JAVA安装
tag: [ ubuntu, java_home]
category: Ubuntu日记
date: 2016-06-24
---

# 关于安装Oracle Java

今天需要安装Oracle的JAVA8，不需要将openjdk卸载，可直接安装oracle java8 installer.

然后为了找到installer把jdk安装到哪了，用which javac找到javac symbolic link，然后一直file，直到找到最后的javac位置.

关于java版本的选择

```bash
sudo update-alternatives --config java
sudo update-alternatives --config javac
```
