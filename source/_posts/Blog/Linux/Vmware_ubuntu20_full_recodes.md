---
title: Vmware安装ubuntu20的过程全纪录
date: 2022-05-07 
comments: true
categories:
- Linux
tags:
- Linux
---

## 前言：

**目的：**  在win10上面的vmware中安装ubuntu20.04的过程全纪录

## 正文：

###  第一步

安装vmware和ubuntu，参考[这个博客](https://zhuanlan.zhihu.com/p/141033713)，记得看那篇博客下面的评论。

在进行第15步的时候，你会发现安装过程巨慢，这是因为使用的是国外的镜像，所以就慢。解决方法就是断网，先进入到系统再说，后面再更换镜像源，使用国内镜像，用命令行更新一下就好了。

### 第二步

装完系统后，第一件事情是更换为国内镜像源。

1. 原文件备份

```
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

2. 编辑源列表文件

```
sudo vim /etc/apt/sources.list
```

3. 将原来文件中内容全删掉，添加下面的内容（清华镜像源）

```shell
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
 
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
 
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
 
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
 
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
 
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
 
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
 
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
 
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
 
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse

```

4. 运行 `sudo apt-get update `，目的是从服务器获取全部可用的、最新的软件包列表，并缓存到本地电脑。
5. 运行 `sudo apt-get upgrade`，该命令会提示你更新软件包，更新就好了。关于 `apt-get update`和 `apt-get upgrade`的区别见这个[链接](https://blog.csdn.net/davidhzq/article/details/102671746#:~:text=%E5%9C%A8Ubuntu%E4%B8%BB%E7%95%8C%E9%9D%A2%E7%82%B9,%E6%9B%B4%E6%96%B0%E5%8D%87%E7%BA%A7%E7%9A%84%E8%BD%AF%E4%BB%B6%E5%88%97%E8%A1%A8%E3%80%82)。

### 第三步

解决win10和ubuntu系统之间，无法使用跨平台copy/paste和drag/drop的问题。参考[这个](https://askubuntu.com/questions/691585/copy-paste-and-dragdrop-not-working-in-vmware-machine-with-ubuntu/824341#824341)，看最高赞回答。

搞好了这一步，就可以实现win10的浏览器中google问题，然后把命令行粘贴到寄生系统ubuntu中。

### 第四步

挂载win10的文件夹到ubuntu中。

进行这一步的前提是进行了第三步中，安装vmware-tools的步骤。然后选择你想要把win10中哪个文件夹共享过去，依次点击左上角虚拟机 --》 设置 --》 选项 --》 共享文件夹 --》 总是启用 --》 添加要共享的文件夹。

设置好之后直接在ubuntu中执行 `vmware-hgfsclient`，来查看已经共享过来的文件夹有哪些，你应该可以看到刚设置好的文件夹。

对该共享文件夹进行测试，分别在win10和ubuntu中新建文件，看对方是否更新。

没问题的话，可以将 `/mnt/hgfs/share`的目录建立一个软连接，放到`/home/用户` 目录下。即执行 `ln -s /mnt/hgfs/share/ /home/用户名/share` 。注意：这几条命令中，读者明白意思就行，需要根据自己情况来修改某些词，当然这步建立快捷方式的过程也不是必须的。。。

