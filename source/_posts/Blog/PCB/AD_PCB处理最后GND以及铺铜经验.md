---
title: AD软件 PCB处理最后GND以及铺铜经验
date: 2022-08-12
comments: true
categories:
- PCB
tags:
- PCB
- AD软件
---

## 前言：

当PCB已经走完其他的线后，就只剩下GND线了。如果什么都不管，直接给所有层都铺上GND的铜的话，当你进行**未连接的走线**检查时，会发现仍旧有一些GND的线没有连上，即仍然显示飞线。这是因为这些GND的焊盘在一些孤岛中，就算你打上GND的小过孔，这些孤岛也连不上。下面讲讲如何处理。

**环境介绍：** AD20

## 正文：

先给那些仍旧有飞线的的GND的焊盘都引出来一点线，然后打一个过孔，就像下面这样。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220812174006978.png" alt="image-20220812174006978" style="zoom:50%;" />

然后选一个合适的层来把上面的小焊盘通过走线连接到孤岛外面的GND上去。

之后 `T-G-A `重新铺所有层的GND铜，再 `T-D-R`运行DRC，检查还剩下哪些飞线没有处理。直到处理完所有的飞线。

最后 `R-B`，只勾选Routing Information，点击Report，来检查连线情况。若是100%了，就OK了。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220812175807896.png" alt="image-20220812175807896" style="zoom:67%;" />
