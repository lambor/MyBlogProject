---
title: 周记总结02-2016.10.29
tag: [ week_note, linux ]
category: 周记总结
date: 2016-10-29
---

#  第2周总结


##  Linux

### No such file or directory

在运行某个bin时,会遇到报"No such file or directory"的错.有一种情况是,在64位环境下运行32位的bin.

解决方案:安装32位的运行库
http://askubuntu.com/questions/133389/no-such-file-or-directory-but-the-file-exists

### 在PATH中添加含有white space的路径

不需要escape white space,所以只需要
```
export PATH=$PATH:"`pwd`"
```

### 关于bash parameter

在escape white space时可以使用
```
tmp="hello there"
tmp=${tmp/\ /}
echo $tmp
```

更多的bash parameter使用在http://pubs.opengroup.org/onlinepubs/009695399/utilities/xcu_chap02.html#tag_02_05_02


## JAVA Concurency

### publish safety



### volatile


