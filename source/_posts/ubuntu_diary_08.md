---
title: Ubuntu日记08-对bash的一些错误认识
tag: [ubuntu,bash,misunderstanding]
category: Ubuntu日记
---

# 对bash的一些错误认识 
**2016.9.1 重庆 阴**

使用bash已经有一段时间了，而且断断续续积累一些使用bash的经验，
但是仍然有一些概念没有搞清楚，所以今天抽空总结纠正一下。

### ">" vs "|"

[What is the difference between “Redirection” and “Pipe”?](http://askubuntu.com/questions/172982/what-is-the-difference-between-redirection-and-pipe)

`cmd1 > tempfile && cmd2 < tempfile` 等价于 `cmd1 | cmd2`
然而使用 `cmd1 > cmd2`，只会创建一个名为cmd2文件，并将cmd1的stdout输出写入cmd2文件。

我的理解是，`>`一端为file，一端为有input或者output的command，而`|`是两端都为command。



### "|" vs "|xargs"

[Why is xargs necessary?](http://superuser.com/questions/600253/why-is-xargs-necessary)

一些command需要以stdin输入，一些command需用args作为输入。

if a command needs argument passed instead of input on stdin you use xargs.


### "strace xxx | head -2" head not work

有时候一些command的输出不能grep或者head等，可能因为该command是通过stderr输出。

此时使用`strace xxx 2>&1 | head -2`。
