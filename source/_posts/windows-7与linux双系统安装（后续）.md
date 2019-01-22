---
title: windows 7与linux双系统安装（后续）
date: 2018-05-27 00:35:45
tags:
---
前两天美滋滋得安装了windows 7下的linux双系统ubuntu，详情见 [链接](https://zhuanlan.zhihu.com/p/37277742) ，以为从此即将开始愉快的学（zhuang）习（bi）之旅了。没想到接下来就是各种强行熟悉其各种命令的噩梦。。。

* * *

首先是各种无法启动

![image](http://upload-images.jianshu.io/upload_images/7094266-acbb7fb00b6400ba.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

于是我选择各种重装，结果悲剧了。

![](http://upload-images.jianshu.io/upload_images/7094266-cfe90c6da4aba864.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

每次重启都是这个，崩溃

于是跟着大神们开始启动救援模式，具体可自行google“grub rescue”这篇是我写文章时打开的 博客 [链接](http://link.zhihu.com/?target=https%3A//blog.csdn.net/u012234115/article/details/38110613)

当我跟着大神们一步步
```
ls （hdx，msdosx）/

set root=hdx，msdosx

set prefix=（hdx，msdosx）/grub

insmod normal

normal
```
终于成功进入grub2界面，即可选择系统（每个人不一样，可以多看看不同博客，有细微差别，我当时尝试了不同格式上述命令，终于属于找到自己电脑的，当你都看完你就都懂了）

此时问题又来了，我进不了ubuntu啊，因为我就是启动不了才发生后续问题的，这个问题至今未解决。。那怎么办，无法更新grub就一直会重启出现grub rescue啊（鬼知道我打了多少遍上面的命令，相信你懂得）我找了各种解决办法，包括什么用尝试启动ubuntu来下载 [引导修复（boot repair）](http://link.zhihu.com/?target=https%3A//blog.csdn.net/u012260238/article/details/52713724) ，但是我ubuntu无法联网啊，U盘也没有（上一篇免U盘装双系统），还有什么live cd，都没有不会啊 （上述情况任何一样有都有相应解决方法，可视情况选择，具体我给的链接应该涵盖了）

在我都打算用grub rescue 作为引导启动项的时候（每次开机打一遍上面的命令），我发现了新的简便方法，只需用到 EasyBCD（装系统时用到）。由于我们可以进入grub2界面进入windows系统，因此操作方便（其实之前一直想尝试用 DiskGenius[参考博客](http://link.zhihu.com/?target=https%3A//blog.csdn.net/pkueecser/article/details/6888392)重建MBR的方法，但是怕windows系统也崩溃。。其实一直最担心的是这个，好多数据的。。结果担心是多余）

了解MBR GRUB 可参考博客 [链接](http://link.zhihu.com/?target=https%3A//blog.csdn.net/jscese/article/details/36865449)

通过EasyBCD 重建MBR 解决grub rescue的问题具体可参考 博客 [链接](http://link.zhihu.com/?target=https%3A//blog.csdn.net/xuehuafeiwu123/article/details/78829717)

当然我的ubuntu还没删，万一哪天高兴打算再研究一下，估计不行的话会删尝试虚拟机的方法，不过可能还是用笔记本破釜沉舟直接安装linux较好，有空在试吧。

本次装双系统花了2个下午加3个晚上，终于成功回到了起点。。。

* * *

本文主要用于个人学习使用，如有侵权请联系我删除。

**参考博客：**

[ubuntu无法启动的解决方法 - CSDN博客](https://blog.csdn.net/xqhrs232/article/details/50967886)
[双系统Ubuntu 引导修复（Boot Repair） - CSDN博客](https://blog.csdn.net/u012260238/article/details/52713724)
[Win7与Ubuntu双系统时【卸载Ubuntu】 - CSDN博客](https://blog.csdn.net/pkueecser/article/details/6888392)
[Win7+Ubuntu双系统，如何卸载Ubuntu系统？ - CSDN博客](https://blog.csdn.net/xuehuafeiwu123/article/details/78829717)
[删除linux系统分区后进windows出现grub rescue（已解决） - CSDN博客](https://blog.csdn.net/u012234115/article/details/38110613)
[Ubuntu--grub rescue 主引导修复 - CSDN博客](https://blog.csdn.net/jscese/article/details/36865449)