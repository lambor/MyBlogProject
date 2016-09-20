---
title: Ubuntu日记05-双击运行bash
tag: [ ubuntu, 双击运行]
category: Ubuntu日记
date: 2016-06-24
---

# 双击运行bash script
**2016.4.12 下午 重庆 阴**

原来使用的是atom editor，但是真的很卡，应该是因为实现方式的原因。atom 就好像是一个super browser.于是我又回到了sublime。

但是ubuntu 下的 sublime有一个bug，不能使用输入法，所以不能使用中文.万能的网友有对应的方法解决该问题：https://github.com/lyfeyaj/sublime-text-imfix。  

但是该解决方法还是有局限性的，只能使用命令行`subl`启动的ST才能使用中文，如果从启动器中启动还是不行。于是我就在桌面建了sublime.sh:  

```bash
#!/bin/bash
subl
```

然后`sudo chmod +x ./sublime.sh`使sublime.sh能够运行。但是双击点开，仍然还是编辑状态。

万能的网友又帮助了我：[ 文件浏览器 Edit -> Preferences -> Behavior. Check "Run executable files when they are opened"](http://askubuntu.com/questions/668079/how-to-make-a-sh-file-executable-by-double-click-in-ubuntu-14-04  )
然后就能双击运行bash script。  

>注：  
>ubuntu中应用的工具栏都是位于屏幕顶端的状态栏上，和Windows有区别。

>总结：  
>我的sublime使用的是sublime3，所以控制台安装Package Control时要注意（ST3好像使用的是python3）。我现在使用的plugin包括：
>Markdown Editing和OmniMarkupPreviewer（超好用，实时的），Terminal。
