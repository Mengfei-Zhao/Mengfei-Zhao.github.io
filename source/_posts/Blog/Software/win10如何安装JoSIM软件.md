---
title: win10如何安装JoSIM软件
date: 2022-04-12
comments: true
tags:
- softwares
categories:
- softwares
---

## 一、前言

这里记录一下在win10上安装JoSIM - Superconducting Circuit Simulator的过程。

**开发环境：**

* win10
* vscode （非必须）
* python 3+
* python 下的 cmake  3.14.4
* Git
* C++ compiler with C++17 support

## 二、开始

[JoSIM官方文档](https://joeydelp.github.io/JoSIM/#microsoft-windows)

将下面两个包下载下来，上面这个是傻瓜版，下载完解压直接用，不用编译出josim-cli.exe和josim.lib了，因为里面已经有了。而下面这个压缩包则是包含源码的工程，例如文档、例子工程等，同样把它解压。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220412183109984.png" alt="image-20220412183109984" style="zoom:80%;" />

先通过python 3.+在该工程下建立一个虚拟环境venv，并激活它。下面就在该虚拟环境中安装一些package。

运行`pip install cmake==3.14.4`

下面安装MSVC（[下载链接](https://visualstudio.microsoft.com/zh-hans/thank-you-downloading-visual-studio/?sku=Community&rel=16)），然后只需要安装带有cmake字样的功能即可，装好后重启电脑。

运行 `cmake --help`，来看是否是如下图所示的样子，新安装的MSVC上有个星号，有的话就往下继续。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220412183851935.png" alt="image-20220412183851935" style="zoom:67%;" />

按照下面的步骤进行

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220412184022288.png" alt="image-20220412184022288" style="zoom:67%;" />

当执行完cmake ..后，会提示一个Git tag标签的错误，这时候要去这个作者github上查看最新的工程的git的hash值，然后复制粘贴到下面的位置。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220412184209683.png" alt="image-20220412184209683" style="zoom:67%;" />

再次cmake ..  就没问题了。

然后把最后一个命令执行了，就会在Release文件夹下产生下面两个东西（这两个东西是和直接下载的另个包中的东西是一致的），然后看官方教程即可。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220412184340677.png" alt="image-20220412184340677" style="zoom:50%;" />

