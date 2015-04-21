---
layout: post
title: Python 变量作用域问题
category: python
tags: Python
keywords: Python 变量作用域
description: 
---



> 刚开始用python写些小工具，边学边摸索，感觉作用域很奇怪 so找了篇文章整了整挂在自己这里了 o(≥v≤)o）

在python中，变量查找遵循LGB原则，即优先在局部作用域(local scope)中对变量进行查找，失败则在全局作用域(global scope)中进行查找,最后尝试再内建作用域(build-in scope)内查找，如果还是未找到的话，则抛出异常。后来由于闭包和嵌套函数的出现，作用域又增加了外部作用域，这样变量的查找作用域优先级变为：局部、外部、全局和内建。 作用域由def、class、lambda等语句产生，if、try、for等语句并不会产生新的作用域。

    def scope1_f1():
   	    def f2():
  	        print local_v
  	    local_v = 'local'
  	    f2()
  	    print global_v
	if __name__ == "__main__":
  	    global_v = 'global'
 	    scope1_f1()

在scope1_f1函数中我们并未对global_str进行赋值（即scope1_f1的局部作用域中并不存在变量lobal_str），但程序正常输出结果'local'和'global'。 
 
### 一 局部作用域中不应对全局变量进行赋值

    需要注意的是虽然我们可以在函数中对全局的变量进行访问，但一旦局部作用域中对全局变量进行了赋值操作，python解释器就不会从全局作用域中查找，而会抛出UnboundLocalError错误。该规则在由局部作用域向外部作用域查找时同样有效。

	def scope1_f1():
    	print global_v               //UnboundLocalError: local variable 'global_v' referenced before assignment
    	global_v = 'local'
	if __name__ == "__main__":
        global_v = 'global'
        scope1_f1()
     
	def scope1_f1():
        print global_v
        global_v.add('local')
	if __name__ == "__main__":
        global_v = ['global']
        scope1_f1()

第一个程序运行error
有资料将该规则描述为&ldquo;局部作用域中全局变量应是只读&rdquo;是不准确的。因为如果变量为list等类型，我们可以通过append这样的方法来修改全局变量，而不影响局部作用域对变量的访问。


### 二 局部作用域中使用 global实现对全局变量进行赋值

如果说确实需要对全局变量进行赋值的话，应在局部作用域中使用global来修饰变量。python2.6中global对变量的修饰可以在函数的任意地方进行，但如果global在赋值之后的话，解释器会提示SyntaxWarning 。

	def scope1_f1():
	     global global_v
	     print global_v
	     global_v = 'local'
	if __name__ == "__main__":
	     global_v = 'global'
	     scope1_f1()

### 三 继承类优先使用第一个基类中的变量

在没有对变量初始化的情况下，继承类会优先使用第一个基类中的变量。下面的例子会输出1而不是2。（说明：如果继承类为初始化函数，会优先调第一个基类的初始化函数，如果前面的基类都没有的话才会调后面基类的初始化函数，初始化函数对变量的修改不在本文讨论范围），

	class sclass1():
	     a = 1
	     def run(self):
	         print self.a
	class sclass2():
	     a = 2
	     def run(self):
	         print self.a
	class dclass(sclass1, sclass2):
	     def run(self):
	         print self.a
	if __name__ == "__main__":
	     a = dclass()
	     a.run()  

### 四 全局作用域指的是本模块而不是程序 

在变量查找时只会在本模块范围内进行变量的查找，即使使用from xxx import 也不会垮模块查找。在python中导入一个模块可以理解为是将另外一个模块各变量赋值给当前模块的同名变量, 对当前模块中变量的赋值不会影响到导入模块的变量。

	main.py
	from module2 import *
	if __name__ == "__main__":
	    module2_v = 5
	    module2_v1 = 3
	    print_modul2()
	modul2.py  
	module2_v1 = 'module2' 
	def print_modul2():
	    print module2_v1
	    print module2_v  

在python中一切都是对象和变量，因此对函数、模块等的的查找同样遵循上面的规则。
最后还存在的一个问题是：使用global可以再局部作用域中对全局变量赋值，那么如何在局部作用域中对外部变量赋值呢？ 目前除了使用list这样的引用传递外我还没发现其他解决方法，留在这里大家一起思考吧。




