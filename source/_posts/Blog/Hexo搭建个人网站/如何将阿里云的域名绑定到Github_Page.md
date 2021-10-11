---
title: 如何将阿里云的域名绑定到Github Page
date: 2021-10-10 12:26:01
tags:
- Hexo
- Github Page
- 个人网站
categories:
- 个人网站
---

### 1、阿里云注册一个域名

### 2、设置域名解析

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211010150234294.png" alt="image-20211010150234294" style="zoom:67%;" />

### 3、添加记录，将域名指向自己的Github Page

首先获得自己的Github Page的IP地址。

```bash
ping username.github.io
```

然后添加一条记录，并按照下图所示设置，A处要填上刚获得的Github Page的IP地址。（这些相关知识点参见[链接](https://blog.csdn.net/qq_29232943/article/details/52786603)）

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211010151013790.png" alt="image-20211010151013790" style="zoom:80%;" />

然后再新建一条记录，记录值要填自己的github.io

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211010151316911.png" alt="image-20211010151316911" style="zoom:80%;" />

设置好了后，应该是看到下面这样，需要看到两记录的状态是正常的才行：

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211010151518680.png" alt="image-20211010151518680" style="zoom:80%;" />

### 4、在Github page中设置

在自己的username.github.io界面，点击Setting，然后直接往下翻，找到GitHub Pages，并进入设置页面。

然后在下面设置域名，并勾选Enforce HTTPS（这个是有加密的，更好些，这样之后自己的网站链接前面是https开头的，如果这里是灰状勾选不了，是因为设置时有问题导致的。），A处就是自己的网站名字。

<img src="https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211010152204074.png" alt="image-20211010152204074" style="zoom:80%;" />

### 5、在hexoSite工程文件中设置

在source文件夹下新建一个名称为CNAME的文件，无后缀。并键入下面这样的东西（记得修改为自己的）：

```yaml
www.zhaomengfei.xyz
zhaomengfei.xyz
```

### 6、然后就是正常的hexo的命令操作

```bash
hexo clean
hexo d -g
```

### 7、最终效果

这样，以后在浏览器中键入`username.github.io`       `zhaomengfei.xyz`       `www.zhaomengfei.xyz时都会自动跳到`https://www.zhaomengfei.xyz 的。

搞定~

