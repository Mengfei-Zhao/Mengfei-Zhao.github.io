---
title: Pycharm在远程Debug时，X11显示图像，matplotlib会报Matplotlib is currently using agg的错
date: 2021-06-10
comments: true
categories:
- Python
- Pycharm
tags:
- Python
- Pycharm

---

开发环境：

* 本地环境win10,  Pycharm2021
* 使用远程的centos7 服务器上的python解释器

Matplotlib会抛出下面的警告，然后用matplotlib画的图也无法显示了。

```bash
UserWarning: Matplotlib is currently using agg, which is a non-GUI backend, so cannot show the figure.
    plt.show()
```

## 在服务器端的配置

首先要检查服务器上的ssh协议是否正常运行，centos7的话是使用 `sudo vim /etc/ssh/sshd_config`来编辑ssh的配置文件，加入下面这样的两行。第一行是开启X11Forwarding，第二行是让默认的Display号为11。这个怎么理解呢？以我的使用场景为例，如果该服务器只有自己一个人用ssh的话，当你开启一个MobaXterm，通过ssh连接到服务器后，我本地电脑分配到的Display号默认就是11了。

```bash
X11Forwarding yes
X11DisplayOffset 11
```

## 在本地机的配置

下面就是只在自己本地机上操作了，用MobaXterm建立ssh的连接（可以设置自动开启X11 Forwarding，这就体现出了它相比于分别操作Putty和X11 ming的优势)。MobaXterm要设置成下面这样，防止ssh休眠，并开启默认开启X11-Forwarding。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220610170025158.png" alt="image-20220610170025158" style="zoom:80%;" />

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220610170133246.png" alt="image-20220610170133246" style="zoom:80%;" />

这样设置好后，当用ssh连接后，会出现下面的信息：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20220610170254450.png" alt="image-20220610170254450" style="zoom:80%;" />

让MobaXterm在后台运行着，这样用Pycharm才可以正常在本地显示figure。记得在Mobaxterm中键入 `echo $DISPLAY`来看本地的号，该号要与下面Pycharm中运行程序的配置文件中的设置的一致，如下图所示。若是这两个号不一致，那么你就会得到本文最开始时的Matplotlib警告信息。

![Snipaste_2022-06-10_17-06-31](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/Snipaste_2022-06-10_17-06-31.jpg)

搞定！
