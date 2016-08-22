---
title: Ubuntu日记06-关于命令行中的空格
tag: [ ubuntu, recovery, passwd]
category: Ubuntu日记
---

# 关于命令行中的空格
**2016.6.30 重庆 雨**

王垠有一篇博客提到过unix like system的缺点，批评它传递参数使用字符串而不是数据结构，导致学习操作很繁杂。
今天我总结一些命令行中空格导致了一些问题。

## `set`命令

比如,`set`等号两边都不能有空格
```
$ set TEST=1
$ set | grep TEST
_=TEST=1
```

左侧有空格，则没有该变量
```
$ set TEST =1
$ set | grep TEST
```

右侧有空格，则也没有改变量
```
$ set TEST= 1
$ set | grep TEST
```

但是右侧**有空格**但没有值，则有该变量
```
$ set TEST =
$ set | grep TEST
_=TEST=
```

比较右侧为空和右侧只有有空格,说明两种情况变量相同
```
$ set TEST_EMPTY=
$ set TEST_SPACE=
$ [$TEST_EMPTY -eq $TEST_SPACE]
$ echo $?
0
```

## 路径中包含空格

```
$ pwd
/media/<USER NAME>/TOSHIBA EXT
```
