draft是草稿的意思，也就是你如果想写文章，又不希望被看到，那么可以
hexo new draft newpage

这样会在source/_draft中新建一个newpage.md文件，如果你的草稿文件写的过程中，想要预览一下，那么可以使用
hexo server --draft

在本地端口中开启服务预览。
如果你的草稿文件写完了，想要发表到post中，
hexo publish draft newpage
就会自动把newpage.md发送到post中。