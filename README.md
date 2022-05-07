master分支是用来hexo部署的，而hexo分支则是自己的总的工程文件，当在一台新电脑上时，只需要按照这个[教程](https://blog.csdn.net/sinat_37781304/article/details/82729029/)配置好环境，把hexo分支clone到本地，即可继续编辑博客了。所以每当deploy一条博客后，都要用git把工程源文件push到远端的hexo分支上。



在hexoSite的文件夹下开一个终端，确认分支为hexo，然后写完博客后，先使用hexo命令把博客推送到个人网站上，然后再使用git命令把hexo分支推送到GitHub上，搞定。



hexo常用命令：

```shell
hexo clean #清除缓存 网页正常情况下可以忽略此条命令
hexo g #生成静态网页
hexo d #开始部署
```



