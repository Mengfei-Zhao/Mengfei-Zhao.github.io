---
title: 如何安装Xic和Wrspice软件
date: 2022-05-07
comments: true
tags:
- softwares
categories:
- softwares
---

这里记录一下在win10上安装Xic Wrspice的过程。

------

先说结论：我最终是在win10上的vmware中的ubuntu上安装了Xic和Wrspice软件。

刚开始看官网和github上有win10上的安装教程，然后操作了一通，没有成功，中间经历了很多坎坷，得出结论，还是上虚拟机中开发吧。。。下面介绍一下我自己的坎坷历程。

### 方案一：在win10上直接安装Xic和Wrspice软件

在[官网](http://wrcad.com/xictools/downld.php?distrib=MINGW)上下载这几个包，然后依次点击安装，装好后就是下面一堆文件，bin文件夹中有所有的启动文件。点击运行软件，你会看到一个终端一闪而过，然后就没有任何动静了。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/202205071559278.png" alt="image-20220507135239293" style="zoom:67%;" />

方案一失败。

### 方案二：在win10的MSYS2中搞Xic和Wrspice的exe文件

参考这个[链接](http://wrcad.com/win_install.html)，上小系统MSYS2，在启动配置并启动Xic和wrspice软件。装好MSYS2后，安装一堆环境包，然后将方案一中的那些 `sw/xictools/`目录挂载到MSYS2系统中的 `/usr/local/xictools/`目录下。当进行到最后一步时，在终端中运行 `winpty program`时，给出了 `Failed to load the program DLL`的报错。参考github中的[该issue](https://github.com/wrcad/xictools/issues/12)，在2022.05.07这一天时，该issue还是open的，官方人员并没有给出有效的解决方案。

最终，方案二也失败。

### 方案三：在win10的MSYS2中编译xic和wrspice的源码

参考[github中的说明](https://github.com/wrcad/xictools)，决定把该github的xic, wrspice源码文件下载下来，在MSYS2中编译这些源码，最终生成.exe文件，我再去启动这些.exe文件，会不会就可以work了呢？试试再说。

它官网给出的说明是使用MSYS2，而github中给出的说明是用Cygwin，这两个东西并不一样，但是我觉得对于编译该xic软件应该没啥区别吧，就还是继续使用了方案二中的MSYS2了。先是下载一堆准备环境，其中还参考了github文档中Linux的说明部分，把该装的都装上了。

最终到了 `make config`的环节，运行以后，给出了类似于下面这样的报错：

```
make[2]: *** No rule to make target 'depend'.  Stop.
```

它的源文件我并没有修改什么，但是看这报错好像是它源码的makefile没有处理好，光解决这个问题，搞了好久，反正就是一个又一个的报错吧。

最终放弃了，方案三失败。

### 方案四：在win10的虚拟机中的ubuntu中安装xic和wrspice的.deb文件

既然品出来了，它原本的源码就是在linux下开发的，那我直接上linux系统应该好一些吧。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/202205071559280.png" alt="image-20220507150335022" style="zoom:67%;" />

从上图中可知好几种linux系统都是可以的，但是由于见到刚上面那个[issue](https://github.com/wrcad/xictools/issues/12)中有人提到用ubuntu装好了软件，所以我也选择了ubuntu，并且选择了和它一模一样的版本。下面开搞！

参考这个[教程](http://wrcad.com/unix_install.html)，下载[这一堆.deb文件](http://wrcad.com/xictools/downld.php?distrib=LinuxUbuntu20)。大家可以参考我的[另一篇博客](https://blog.csdn.net/weixin_43128203/article/details/124632496?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22124632496%22%2C%22source%22%3A%22weixin_43128203%22%7D&ctrtid=C1MBm)，来装vmware和ubuntu。装好ubuntu后，将win10下的xic的.deb的安装包所在文件夹挂载到虚拟机的ubuntu中，在终端中安装即可。当跟着官网的说明搞完后，就可以正常启动xic, wrspice软件了。

成功！

