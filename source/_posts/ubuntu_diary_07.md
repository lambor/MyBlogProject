---
title: Raspberry日记01-树莓派开wifi热点
tag: [ raspberry, wifi, hotspot ]
category: Raspberry日记
date: 2016-06-30
---

# Raspberry 

## PI到手

2014.8.25 下午 快递到，组装了亚克力盒子，安装了系统，初始了系统。

## 内网连PI

使用Advanced IP Scanner V2搜索其内网的ip,然后通过putty进行SSH连接到PI

## 外网连接PI

http://blog.csdn.net/kongdefei5000/article/details/19137125
参考其方法，使得PI连接外网，并通过putty安装了vnc，进行图形桌面连接

## 无线wifi连接

http://www.educity.cn/wenda/565819.html
http://blog.sina.com.cn/s/blog_488a3b1e0101ajw0.html

通过wifi设置后的PI，只要启动前插上网线，仍能 使用方法2(通过PC，PI分别网线连接路由器，使用putty内网登陆）和方法3(PC和PI网线连接，PC无线连wifi，用putty外网登陆？)

## ubuntu登陆PI
使用nmap查询PI的IP，ubuntu已安装openssh-client，使用命令ssh pi@*<ip>**登陆
同时安装使用vncviewer来桌面远程连接PI，命令是vncviewer

```
nmap -sT -p 22 -oG - 172.24.106.* | grep open
```

nmap命令使用http://www.2cto.com/Article/201102/84402.html

