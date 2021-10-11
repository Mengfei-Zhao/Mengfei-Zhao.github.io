---
title: Arduino舒适的开发环境搭建：vscode+PlatformIO
date: 2021-10-09 23:26:01
comments: true
tags:
- Arduino
- vscode
- PlatformIO
categories:
- vscode
- Arduino
---

## 一、前言

Arduino自带的IDE用在小的工程时还可以应付，但是面对大型工程时，就比较鸡肋了。本着想愉快的编写Arduinio的代码，让我们开始“折腾”吧~

**开发环境：**

* win10
* vscode + PlatformIO插件
* Arduino 官方的IDE  1.8.16
* 手头有一个Arduino UNO板卡
* 该博客中的某些链接需要梯子呦

## 二、开始

首先下载、安装vscode。然后安装platformio插件，如下图：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007173651871.png" alt="image-20211007173650230" style="zoom:70%;" />

这个插件在使用IDE新建工程时，有些bug，就是特别慢，网上说是需要从github上下载一些东西，所以就很慢，而国内在使用github时有时候就是挺慢的。不过还是想用这么香的东西，肿么办呢？且听我慢慢道来。

### 使用IDE方式新建helloworld工程：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007174311073.png" alt="image-20211007174311073" style="zoom:80%;" />

首先点击如图所示的，更新一下pio core，下面是官方的介绍（[官方文档链接](![image-20211007174534039](C:/Users/meng/AppData/Roaming/Typora/typora-user-images/image-20211007174534039.png)![image-20211007174534039](C:/Users/meng/AppData/Roaming/Typora/typora-user-images/image-20211007174534039.png))），小伙伴记得仔细看官方文档呦。

![image-20211007174451940](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007174451940.png)

然后点击下面的New Project。

![image-20211007174714097](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007174714097.png)

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007174912757.png" alt="image-20211007174912757" style="zoom:80%;" />

这里在选择工程路径时，有时加载会有些慢。然后点击底部的Finish，之后会加载一段时间，这个时间真是很奇怪，快时只需要几秒钟，慢时一个小时也搞不定。慢时我后面会讲如何应对。

![image-20211007175216973](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007175216973.png)

之后窗口中会出现两个相同的文件夹，需要右击任意删除一个（点击Remove folder from workspace）。之后save as一个workspace。

![image-20211007175724408](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007175724408.png)

处理之后一定要确保左侧的工作空间窗口中像上图这样，即一个workspace下面只有一个helloworld4的工作目录。如果是像下面这样嵌套的路径结构或者其他的结构，后面在编写源文件时，可能会出现头文件引用找不到的问题，即例如右侧B处的Serial下面有个红色波浪线，提示找不到该玩意儿在哪里。。。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007180030141.png" alt="image-20211007180030141" style="zoom:80%;" />

而这点是vscode中c/c++插件的一个bug（详情参见此[链接](https://community.platformio.org/t/include-errors-detected/5858)），只要想办法绕过此bug即可。

![image-20211007180741703](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007180741703.png)

当然若实在是头文件引用错误的话，可以暴力点，关闭所有的错误提示，从此再无红色波浪线（设置看此[链接](https://blog.csdn.net/HermitSun/article/details/103627053#:~:text=%E9%94%99%E8%AF%AF%E6%8F%90%E7%A4%BA%E4%BA%86%E3%80%82-,%E5%90%AF%E7%94%A8%E6%96%B9%E6%B3%95%E6%98%AFctrl%2Bshift%2Bp%20%E6%90%9C%E7%B4%A2%E5%90%AF%E7%94%A8%E9%94%99%E8%AF%AF%E6%B3%A2%E5%BD%A2,%E6%9B%B2%E7%BA%BF%EF%BC%8C%E6%89%93%E5%BC%80%E5%B0%B1%E8%A1%8C...&text=%E4%BB%A3%E7%A0%81%E5%87%BA%E7%8E%B0%E6%B3%A2%E5%BD%A2%E6%9B%B2%E7%BA%BF%EF%BC%9A%20%E8%A7%A3%E5%86%B3,%E6%94%B9%E4%B8%BAtrue%E5%8D%B3%E5%8F%AF%E3%80%82)）。

**编写源代码：**

下面是让LED灯闪烁，并发送数据到串口。

main.cpp:

```c++
#include <Arduino.h>
#define onboard 13

void setup()
{
  // put your setup code here, to run once:
  pinMode(onboard, OUTPUT);
  Serial.begin(9600);
}

void loop()
{
  // put your main code here, to run repeatedly:
  digitalWrite(onboard, LOW);
  delay(1000);
  digitalWrite(onboard, HIGH);
  delay(1000);
  Serial.println("Hello World!");
}
```

对了，arduino的代码其实就是C++代码，当然可以分成很多个子.cpp，.h来编写代码，参考[链接1](https://www.eefocus.com/liusk2014/blog/14-05/303449_fe78d.html)， [链接2](https://blog.csdn.net/codalion/article/details/86014560)。

**编译，烧录：**

![image-20211007181612585](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007181612585.png)

上图中A是编译，B是烧录，C是打开串口工具。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007181950115.png" alt="image-20211007181950115" style="zoom:80%;" />

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007182127853.png" alt="image-20211007182127853" style="zoom:80%;" />

下面是串口中的数据：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007182330671.png" alt="image-20211007182330671" style="zoom:80%;" />

**搞定！**



### 若通过IDE方式来创建工程，很慢的话，请接着往下看

首先看下这个[链接](https://community.platformio.org/t/too-slow-to-create-a-new-project/18259)。

可以通过CLI的方式来创建工程，用vscode打开一个空文件夹，然后在terminal中敲入 `pio project init --board uno`，然后会在vscode中释放一堆一样的文件夹结构（*这个过程会快一些吧*），然后打开这个platformio工程，此时看下platformio.ini文件中是否正确，如下所示。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211007183715444.png" alt="image-20211007183715444" style="zoom:80%;" />

现在新建并编写自己的源文件即可。



ps: 给个油管的PIO开发arduino的[教程](https://www.youtube.com/watch?v=lXchL3hpDO4&ab_channel=JanPenninkhof)。



**最后：**

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/点赞.gif" alt="点赞" style="zoom: 50%;" />

