# 面向对象

### 封装

	对一些对象内部成员,不想暴露在外边的成员私有化,隐藏内部实现
	
	在设置实体类的时候可以保证数据的完整性

### 继承

	继承破坏了低耦合的概念
	
	在已存在的类上做进一步的扩展,提高开发效率,达到代码重用效果

### 多态

```
两种形式实现多态:接口、继承、抽象
```

## 七大设计原则

### 单一职责原则又称单一功能原则

一个模块只负责一个功能,减少模块和模块之间的耦合,让模块专注单一功能

#### 好处:

	业务一般是经常变化的,业务变化肯定模块内代码也会改变,如果耦合度高的情况下,一**个模块内代码改变可能需要涉及到很多模块代码都需要改变**,这时候又需要新的一轮测试来测试这些模块可能出现的问题.耦合度低自然没有这个问题

### 开闭原则

	模块应该是对扩展开放,对修改源代码关闭的原则,在不修改这个模块的前提下进行扩展,简化后期维护过程

好处:



#### 好处:

	可扩展:	简化后期维护过程		
	
	关闭修改:	提高程序的稳定性,保证其他模块可以正常使用这个模块,
	
		如果这个模块可以被随便修改,那当修改完成后,可能导致其他模块不能正常使用这个模块





