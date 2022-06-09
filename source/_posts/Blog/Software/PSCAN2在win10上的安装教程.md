---
title: PSCAN2在win10上的安装教程
date: 2022-04-09 
comments: true
tags:
- softwares
categories:
- softwares
---

## 一、前言

目的：在win10上安装PSCAN2 Superconductor Circuit Simulator软件。

**开发环境：**

* win10
* vscode + python插件 + vhdl插件

## 二、开始

查看官网要求：[官网链接](http://www.pscan2sim.org/install.html)

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220409173851493.png" alt="image-20220409173851493" style="zoom:80%;" />

可以看到是安装32 bit的anaconda，所以打开[Anaconda网站](https://www.anaconda.com/products/distribution)，往下翻，找到32 bit的windows安装包。可以看到写下这篇博客时，Anaconda已经更新到了Python 3.9，而PSCAN2要求的python环境是3.8的，这个版本差异我是通过后续在Anaconda软件内新建3.8版本的python环境来解决的，所以这里就直接下载这个Python3.9 32bit 的安装包即可。下载好了后，安装，参考这个[Anaconda安装教程](https://www.youtube.com/watch?v=kQMPPLRpuI0&ab_channel=Koolac)。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220409174028048.png" alt="image-20220409174028048" style="zoom:60%;" />

anaconda安装好了后，要是没有将它加入到环境变量，需要加入到环境变量，否则无法在terminal中执行conda命令，参考[这个](https://www.py.cn/tools/anaconda/19876.html#:~:text=%E6%B7%BB%E5%8A%A0anaconda%E5%88%B0%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F%E7%9A%84%E6%96%B9%E6%B3%95%EF%BC%9A%E9%A6%96%E5%85%88%E8%BF%9B%E5%85%A5anaconda,%E6%B7%BB%E5%8A%A0Scripts%E8%B7%AF%E5%BE%84%E5%8D%B3%E5%8F%AF%E3%80%82&text=%E5%A4%8D%E5%88%B6%E5%BD%93%E5%89%8D%E8%B7%AF%E5%BE%84%EF%BC%9B-,%E6%8E%A5%E7%9D%80%E6%89%93%E5%BC%80%E7%B3%BB%E7%BB%9F%E9%AB%98%E7%BA%A7%E8%AE%BE%E7%BD%AE%EF%BC%8C%E8%BF%9B%E5%85%A5%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F%E8%AE%BE%E7%BD%AE%EF%BC%9B,%E6%B7%BB%E5%8A%A0Scripts%E8%B7%AF%E5%BE%84%E5%8D%B3%E5%8F%AF%E3%80%82)。

接下来新建一个python 3.8的环境（按照pscan2 的官网要求），参考[这个](https://blog.csdn.net/H_O_W_E/article/details/77370456)，在这篇教程中的py36可以自定义的，当然我们这里需要新建成3.8，而不是3.6的。

接下来将[pscan2网站](http://www.pscan2sim.org/downloads.html)的所有东西下载下来，即下面这些东西，留着用来学习吧。假设我们下载到了一个名叫 `pscan2`文件夹，并将这所有的压缩包类的都解压到该目录下。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220409175516063.png" alt="image-20220409175516063" style="zoom:67%;" />

在 `pscan2`文件夹中，开一个终端，在终端中切换到我们的python3.8环境，然后执行 `conda install pscan2-xxx.bz2`命令，目的是将pscan2软件部署到该Python环境中，接下来就可以启动pscan2软件了。

在上面的终端中，cd到testnot文件夹（这里面是一个demo工程，详情见pscan的两个pdf手册），然后键入下面图片中的命令 `python -m pscan2.gui testnot`，幸运的话，你就能正常启动软件了，并看到GUI软件出现。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220409180000361.png" alt="image-20220409180000361" style="zoom:67%;" />

### 遇到了一个bug:

我在执行上述命令后，遇到了下面这样的错误：（参考的是[这个](https://stackoverflow.com/questions/28165639/unicodedecodeerror-gbk-codec-cant-decode-byte-0x80-in-position-0-illegal-mult)）

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220409180406876.png" alt="image-20220409180406876" style="zoom:67%;" />

解决办法，打开这个LodaCircuit.py文件，在报错的这一行（如下图所示）进行修改，加入这个 `, encoding='UTF-8' `，然后保存。再执行一次该命令 `python -m pscan2.gui testnot`，这次应该就可以正常启动pscan的GUI了。GUI如下所示。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220409180518536.png" alt="image-20220409180518536" style="zoom:67%;" />

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220409180743357.png" alt="image-20220409180743357" style="zoom:67%;" />

**最后：**

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/点赞.gif" alt="点赞" style="zoom: 50%;" />

