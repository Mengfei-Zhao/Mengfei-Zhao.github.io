master分支是用来hexo部署的，而hexo分支则是自己的hexo工程文件，当在一台新电脑上时，只需要按照这个[教程](https://blog.csdn.net/sinat_37781304/article/details/82729029/)配置好环境，把hexo分支clone到本地，即可继续编辑博客了。所以每当deploy一条博客后，都要用git把工程源文件push到远端的hexo分支上。

hexo命令：
hexo clean 清除缓存
hexo g 生成
hexo d 部署
hexo s 用来本地查看网页

Git命令：
gst
gaa
gcz
git push origin hexo  将hexo分支push到远端

git pull origin hexo 