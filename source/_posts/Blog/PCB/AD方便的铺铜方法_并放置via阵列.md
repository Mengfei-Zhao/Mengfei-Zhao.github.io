---
title: AD软件方便的铺铜，并放置via阵列
date: 2021-10-12 
comments: true
categories:
- PCB
tags:
- PCB
- AD软件
---

## 前言：

**环境介绍：**AD20

**目的：**将PCB两面都铺上GND的铜，并放置via阵列。

## 正文：

当把板子都布局，布好线后，需要铺铜时，`P->G`，然后选择铺铜的区域，围绕板子四周画一个矩形，画好后，鼠标右键2下，铺铜。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211012164220558.png" alt="image-20211012164220558" style="zoom:67%;" />

铺好后手动去除板子四个角外部的铜，如下图所示，选择Polygon Pour Cutout，然后把不想要的铜圈起来即可。选中铜皮，将其设置为连接到GND net上。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211012164527955.png" alt="image-20211012164527955" style="zoom:67%;" />

上面只是铺好了top layer的铜皮，下面来铺bottom layer的。选中top layer的铜皮，ctrl+c，然后鼠标左键点击一下我们设置好的origin point，切换到bottom layer，选择special paste，然后对话框设置一下，之后再选择一次origin point即可。之后可以再按照上述方式去除一下keep out外面的死铜。当然也可以在铺铜的设置选项里勾选“去除死铜”，但是这样会把板子里面的死铜也给去除掉，读者根据需要来选择吧。



<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211012165114319.png" alt="image-20211012165114319" style="zoom:80%;" />

下面开始放置一些小的via阵列，首先将“铜皮”隐藏，放置干扰我们视野。方法：ctrl+D，在view configuration窗口中隐藏Polygons。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211012165745814.png" alt="image-20211012165745814" style="zoom:80%;" />

开始放置via阵列：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211012165946987.png" alt="image-20211012165946987" style="zoom:80%;" />

先设置一下Net为GND，然后去勾选左上角的Constrain Area来选择放置的区域，根据需要设置间距，大小之类的参数。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211012170045704.png" alt="image-20211012170045704" style="zoom:80%;" />

放好via阵列的样子：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211012170315201.png" alt="image-20211012170315201" style="zoom:67%;" />

之后将铜皮取消隐藏即可，并布置丝印层。
