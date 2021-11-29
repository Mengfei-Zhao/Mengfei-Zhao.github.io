---
title: Python_多继承时_父类之间竟然可以相互调用method
date: 2021-11-09
comments: true
categories:
- Python
tags:
- Python
---

```Python
#!/usr/bin/env python
# -*- coding:utf-8 -*-

class B(object):
	def func_b(self):
		print("In class B, func_b")
		# print('B: ', B.__mro__)
		print('B: ', self)
		self.func_d()  # 调用同为父类的D中的func_d函数


class C(object):
	def func_c(self):
		self.func_b()
		print('C: ', self)
		# print('C: ', C.__mro__)
		print("In class C, func_c")


class D(object):
	def func_d(self):
		print('D: ', self)
		# print('D: ', D.__mro__)
		print("In class D, func_d")


class A(B, C, D):  # A同时继承B,C,D
	def __init__(self, parent=None):
		super(A, self).__init__()
		print('A: ', self)
		# print('A: ', A.__mro__)

	def func_d(self):
		print("In class A, func_d")


if __name__ == '__main__':
	A_inst = A()
	print('A_inst: ', A_inst)
	A_inst.func_b()
	A_inst.func_c()
	A_inst.func_d()
```

上面B,C,D都是A的父类，互为平行关系，而C类中的func_c竟然可以调用B类中的func_b？？？程序运行结果如下，可以看到**类实例A_inst**和**A, B,C,类中的self**是一个内存地址，这也就解释了为何C类中的func_c竟然可以调用B类中的func_b。

```bash

A:  <__main__.A object at 0x000002D60CE2E070>
A_inst:  <__main__.A object at 0x000002D60CE2E070>
In class B, func_b
B:  <__main__.A object at 0x000002D60CE2E070>
In class A, func_d
In class B, func_b
B:  <__main__.A object at 0x000002D60CE2E070>
In class A, func_d
C:  <__main__.A object at 0x000002D60CE2E070>
In class C, func_c
In class A, func_d
```



**知识点：**有self时，该方法是绑定到对象的方法。

```python
class Person(object):
    def func01(self):
        print('绑定到对象的方法')
    
    @classmethod
    def func02(cls):
        print('绑定到类的方法')
    
    @staticmethod
    def func03():
        print('非绑定方法')
```



参考：

[Python 类方法实例方法内存地址相同???]: https://www.jianshu.com/p/9e947014549f

