---
title: AD软件_PCB板的四个角放置通孔和圆弧keepout线的快捷方法
date: 2021-10-15
comments: true
categories:
- PCB
tags:
- PCB
- AD软件
---

## 前言：

**环境介绍：** AD20

## 正文：

在开始画PCB时，先用keepout线画一个矩形，把origin点设置到角落里。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211015224400882.png" alt="image-20211015224400882" style="zoom:50%;" />

然后放置一个通孔（用于安装螺丝，来固定板卡），并设置通孔的坐标为一个（-3.3mm, 3.3mm），这个距离自己掌握，但必须x,y绝对值相等。

选中通孔，`ctrl+c`，出来绿色十字架时，点一下origin（以Origin）为复制参考点。点击另外的三个角，`ctrl+v`，出现绿色十字架时，按下空格来旋转，然后点击板卡的顶点。搞定！

之后在四个角画keepout圆弧，选择圆弧工具：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211015225053567.png" alt="image-20211015225053567" style="zoom:68%;" />

出现绿色十字架，点击一下通孔的圆心：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211015225331348.png" alt="image-20211015225331348" style="zoom:50%;" />

然后点击**大圆**与**矩形边**相切的位置，如下图（我们只需要右下角的**四分之一圆弧**）：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211015225543912.png" alt="image-20211015225543912" style="zoom:50%;" />

之后删除多余的矩形的**角**，就得到这样的了。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211015225807361.png" alt="image-20211015225807361" style="zoom:50%;" />

然后选中这个**四分之一圆弧**，以通孔圆心为参考点，复制，粘贴处其余3个角。

搞定！

