---
title: ZYNQ开发学习笔记（一）：BOOT.bin，fsbl文件，将程序固化到板上的QSPI_Flash中
date: 2021-10-10 13:26:01
comments: true
categories:
- ZYNQ
tags:
- ZYNQ
---

## 1、环境介绍：

* ZYNQ-7000 MZ7XA板卡
* vivado 2020.1
* vitis 2020.1

## 2、正文：

首先介绍一下[镜像](https://baike.baidu.com/item/%E9%95%9C%E5%83%8F%E6%96%87%E4%BB%B6/101053?fr=aladdin)这个概念，下面是百度百科中的解释：

> 所谓镜像文件其实和rar ZIP压缩包类似，它将特定的一系列文件按照一定的格式制作成单一的文件，以方便用户下载和使用，例如一个操作系统、游戏等。它最重要的特点是可以被特定的软件识别并可直接刻录到[光盘](https://baike.baidu.com/item/光盘/170215)上。其实通常意义上的镜像文件可以再扩展一下，在镜像文件中可以包含更多的信息。比如说系统文件、[引导文件](https://baike.baidu.com/item/引导文件/659617)、[分区表](https://baike.baidu.com/item/分区表/215102)信息等，这样镜像文件就可以包含一个分区甚至是一块硬盘的所有信息。

额，理解了镜像的概念，接下来以在vivado vitis工程中的实际操作中学习BOOT.bin  fsbl等内容。

### vivado工程方面：

配置一下PS，生成一个HDL Wrapper.v，然后在Wrapper.v文件中加入一段4bit流水灯的代码，代码如下：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002162341338.png" alt="image-20211002162341338" style="zoom:67%;" />

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002162649052.png" alt="image-20211002162649052" style="zoom:70%;" />

然后生成.bit文件，导出xsa文件，接下在切换到vitis开发。

### vitis工程方面：

新建一个硬件工程，命名为`run_led_hw_platform`

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002163328456.png" alt="image-20211002163328456" style="zoom:67%;" />

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002163622228.png" alt="image-20211002163622228" style="zoom:80%;" />

指定刚vivado生成的xsa文件，上图中记得勾选Generate boot components，这个会在生成的硬件工程中产生一个zynq_fsbl文件夹，打开会发现有一堆fsbl相关的源文件，编译一下整个硬件工程，就会在下面图二的1处产生一个fsbl.elf文件。

![image-20211002164114451](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002164114451.png)

![image-20211002164030549](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002164030549.png)

接下来新建一个helloWorld的应用工程，命名为`helloWorld`，并编译一下。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002164344390.png" alt="image-20211002164344390" style="zoom:80%;" />

![image-20211002164607517](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002164607517.png)

接下来讲一下当我们成功固化程序到flash中后，ZYNQ板子启动的过程。

* ZYNQ内部的BootROM存储有一段在CPU复位后固定执行的代码。称为stage-0启动代码。（这个ROM中的代码，掉电不丢失）

* 这段代码用来配置一个ARM CPU和一些必要外设，从而能从一个启动设备中获取FSBL（first stage boot loader）执行。BootROM是一个ROM，不可写，PL的配置不是通过BootROM实现的。BootROM不能使用DDR和SCU，因为它们还没有初始化。

* BOOT.bin是一个镜像文件，我们这里是将它存储在外部的QSPI-Flash中，BOOT.bin包含有fsbl.elf，PL部分配置文件（.bit)，应用工程的可执行二进制文件（helloWorld.elf文件）

  ![ ](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/20200626232927148.png)

* 当BootROM把flash中BOOT.bin中的fsbl装载到OCM后，接下来就开始执行fsbl了。

* fsbl负责下面这些：

  <img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002172924391.png" alt="image-20211002172924391" style="zoom:80%;" />

  对于基于zynq的嵌入式Linux系统，BootROM引导启动FSBL，FSBL引导启动U-Boot，U-boot引导启动Linux内核。

理解了上面这些，接下来继续创建Boot Image。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002171139341.png" alt="image-20211002171139341" style="zoom:80%;" />

上图中出现了好多文件，它们的关系详情请参考ug821的boot章节，这个BOOT.bin就是需要制作出来的镜像文件，它里面包含有下面fsbl.elf，run_lef.bit，helloWorld.elf文件。至于上面的helloWorld.bif文件，它是一个Boot Image Format 文件，用于制作BOOT.bin用的。

![image-20211002173806240](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002173806240.png)

制作好BOOT.bin后，接下来把它烧录到QSPI-Flash中：

![image-20211002174044195](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002174044195.png)

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002174241139.png" alt="image-20211002174241139" style="zoom:90%;" />

在consol窗口中出现一系列消息后，就成功了。

![image-20211002174408697](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002174408697.png)

此时打开一个串口窗口，对板子重新上电，可看到流水灯在闪烁，串口打印成功。

![image-20211002174626648](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211002174626648.png)

## 3、参考文献：

* [米联客教程](https://blog.csdn.net/jinry001/article/details/99693549)
* [ZYNQ_FSBL学习](https://blog.csdn.net/asd1147170607/article/details/106976572)
* [zynq中的BootROM](https://blog.csdn.net/qq_43445577/article/details/113846028)

