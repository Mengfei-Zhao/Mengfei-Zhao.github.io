---
title: Python_使用GUI和多线程时报错
date: 2021-11-29
comments: true
categories:
- Python
tags:
- Python

---

开发环境： win10,  Pycharm2021

这里记录一下解决该问题的历程。该工程中使用到了PyQt5的GUI，多线程技术等。使用pycharm，在程序运行时，程序偶尔会莫名奇妙的退出，并**只是**报下面的错误：

```python
Process finished with exit code -1073741819 (0xC0000005)
```

纳尼，只是给出了这一个报错，却没有任何traceback？？！（**想直接看结论的请下滑到底**）并且这个报错只是偶尔才会给出。上网搜索上面这个报错，查到了[这个](https://stackoverflow.com/questions/33582766/process-finished-with-exit-code-1073741515-0xc0000135)，按照其给出的方法试了试：

![image-20211129214434686](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211129214434686.png)

![image-20211129214525252](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211129214525252.png)

于是查看win10的**事件管理器**，发现了下面的报错信息，而这些竟然在pycharm中完全不显示。由下面看出来应该是pyqt5引起的报错，于是重新安装了pyqt5，报错并没有解决。

![image-20211129214749891](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211129214749891.png)

又上网搜索该 **事件管理器**中的报错，没有解决问题。

------

于是又上网搜索 **pycharm come across error without traceback**，终于努力对了方向。找到了[这个](https://intellij-support.jetbrains.com/hc/en-us/community/posts/207319305-No-stack-trace-printed-after-exception)，按照下面这种方法试了试，终于在debug时给出了具体的 **traceback**。

![image-20211129215454501](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211129215454501.png)

Debug的Console中给出的具体的报错如下，而且在程序靠前的某处还给出了一个警告，但是并没有影响程序的往下执行。

```python
警告如下：
QObject::setParent: Cannot set parent, new parent is in a different thread

--snippets--

报错如下：
QObject: Cannot create children for a parent that is in a different thread.
(Parent is QTextDocument(0x18992e5ad60), parent's thread is QThread(0x18990b3af30), current thread is QThread(0x18993804600)
```

于是上网搜索这两个报错，发现了[link1](https://forum.qt.io/topic/68530/about-the-right-way-to-use-qthread-error-cannot-create-children-for-a-parent-that-is-in-a-different-thread/4), [link2](https://stackoverflow.com/questions/3268073/qobject-cannot-create-children-for-a-parent-that-is-in-a-different-thread), [link3](https://forum.qt.io/topic/78994/error-qobject-setparent-cannot-set-parent-new-parent-is-in-a-different-thread)：

![image-20211129220318194](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211129220318194.png)

![image-20211129220554350](https://jasonbourne-photo1.oss-cn-beijing.aliyuncs.com/img1/image-20211129220554350.png)

看完后有了灵感，总之是pyqt5的GUI和多线程导致的报错。于是上网搜索 **pyqt5 qthread**关键词，找到了一个令人欣喜若狂的文章：**[戳我](https://realpython.com/python-pyqt-qthread/#conclusion)**。该文章中还讲了python的线程和QThread的比较。看完后完全明白了，上面的这些警告和报错是如何产生的。我的程序是先运行windows的部分，此时是在mainThread里，然后在mainThread里又开了一个python的thread去处理mainThread里的一些objects和widgets，而每当要访问这些widgets的地方都会抛出上述的**警告和错误**。

然后按照该文章，比葫芦画瓢就好了。搞定~

