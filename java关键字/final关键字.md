####**前言：**
在前面的文章中，我们介绍了static关键字的作用，现在，我们一起来聊一下final关键字。

首先，关于final关键字，我们提出三句话：

 1. 被final修饰的变量是不可以改变的
 2. 被final修饰的方法不可以被重写
 3. 被final修饰的类不可以被继承

----------

在《java编程思想》中，有这样一句话，“这是无法改变的”。这里，我们讨论使用final的三种情况：**数据、方法和类**。

####**1、final数据：**
1）一个永不改变的编译时常量。在Java中，这类常量必须是基本数据类型，并且以关键字final表示。**final成员变量必须在声明的时候初始化或者在构造器中初始化，否则就会报编译错误。**

![这里写图片描述](http://img.blog.csdn.net/20170323094303573?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSExLXzExMzU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

```
package com.hlk;

import java.util.Random;

class Value {
	int i;
	public Value(int i) {
		this.i = i;
	}
}

public class Final_Test {
	
	private static Random random = new Random(100);
	private String id;
	
	public Final_Test() {
	}
	public Final_Test(String id) {
		this.id = id;
	}
	public String getId() {
		return id;
	}
	public void setId(String id) {
		this.id = id;
	}
	
	private final int valueOne = 10;
	private static final int valueTwo = 10;
	public static final int valueThree = 30;
	private final int i4 = random.nextInt(20);
	static final int i5 = random.nextInt(30);
	
	private Value v1 = new Value(11);
	private final Value v2 = new Value(22);
	private static final Value v3 = new Value(33);
	
	//Arrays:
	private final int[] a = {1,2,3,4,5,6};
	
	@Override
	public String toString() {
		return "i4 = " + i4 + ",i5 = " + i5;
	}
	
	public static void main(String[] args) {
		Final_Test f1 = new Final_Test();
		
		//f1.valueOne++;  报错，因为final定义的数据不可改变
		f1.v2.i++;
		f1.v3.i++;
		
		System.out.println(f1);
		System.out.println("f1.v2.i: " + f1.v2.i);
		System.out.println("f1.v3.i: " + f1.v3.i);
		
		/**
		 * 引用的内容可以改变，但是引用不可以被改变
		 */
		final Final_Test id1 = new Final_Test("id1");
		final Final_Test id2 = new Final_Test("id2");
		
		id1.setId("change_id1");
		System.out.println(id1.getId());//id1被改变
		
		//id1 = id2;//报错The final local variable id1 cannot be assigned.
	}
}
```

对于基本数据类型，final使数值恒定不变；而用于对象引用，final使引用恒定不变。一旦引用被初始化指向一个对象，就无法再把它改为指向另一个对象。


**重点：**
在这里，我们提出一个问题，这里所说的被final修饰的变量不可以被改变，是什么不可以被改变？变量的内容？还是变量的引用？
**答：**根据上面的内容，我们可以看出，**被final修饰不可变的是变量的引用，而不是引用指向的内容，引用指向的内容是可以改变的**。


####**2、final方法：**
**父类的final方法是不能被子类所重写的，也就是说子类是不能够存在和父类一模一样的方法的。**


####**3、final类：**
在开发中，出于安全或者其它原因考虑，我们不希望该类被继承，就使用final来修饰。





