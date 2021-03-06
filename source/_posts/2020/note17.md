---
title: java 语言入门
date: 2018-01-29 20:52:02
tags:
- Java
categories:
- Java
---


**Java使用人数最多的跨平台面向对象开发语言**

请看下面的例子：

```public class MyFirstJavaProgram
{
	public static void main(String[] args)
	{
		System.out.println("Hello World!");
	}
}
```
<!-- more -->

## Java基础

J2EE是为企业级应用程序设计的，J2ME是为移动应用程序设计的。

Sun公司将新的J2版本分别命名为Java SE,Java EE,Java ME。

Java承诺“ **编写一次，到处运行** ”。

Java是：

1. **面向对象的**： 在Java中所有的东西都是一个对象。
2. **平台独立的**：当Java被编译时，它并不是编译到特定的机器中，而是用平台独立性的字节码编译。这种字节码在网页上是分布式存储的，并且可以在不同的平台通用的虚拟机上运行。
3. **简单的**：Java是为了易于学习而设计的。
4. **安全的**。
5. **体系结构中立的**：Java编译器可以生成一个结构中立的对象文件格式，他能够使被编译过的代码在Java运行系统存在的情况下在很多进程中运行。
6. **便捷的**：由于Java的结构中立性以及它的运行不受限制的特征使得它十分便捷。
7. **稳健的**。
8. **多线程的**。
9. **易于理解的**。
10. **高性能的**。
11. **分布式的**。
12. **动态的**。

***

### Java历史

Sun公司于1995年发行第一个公开版本Java1.0。

### Java环境设置

你在电脑上安装完Java之后，你需要将环境变量设置到指定目录。

### Java 编辑器

在编写Java程序时，你需要一个文本编辑器。


## Java基本语法

Java应用程序可以被定义为对象的集合，这些对象通过调用各自的方法来进行通信。

1. **对象**：对象具有状态和行为，对象是类的一个实例。
2. **类**：类可以被定义为描述对象所支持的类型的行为和状态的模型或蓝图。
3. **方法**：方法是一种基本的行为。
4. **实例变量**：每个对象都有它的特殊的实例变量的集合，一个对象的状态是由那些实例变量所被赋的值所决定的。

### 第一个Java程序

```
public class MyFirstJavaProgram
{
	/*This is my first java program.
	 *This will print "Hello World!" as the output
	 */
	public static void main(String[] args)
	{
		//prints Hello World
		System.out.println("Hello World!");
	}
}

```

### 基本语法

1. **大小写敏感性**。
2. **类的命名**：首字母大写。
3. **方法的命名**：首字母小写。
4. **程序文件名**：必须和类的名称匹配。
5. **public static void main(String []args)**：这个方法是Java程序的强制性部分。

### Java标识符

Java的所有的组成部分都要有自己的名称。类，变量和方法的名称称为标识符。

1. 以字母，货币字符（$）或者下划线（_）开头。
2. 不能使用关键字。

### Java关键字

|关键字|关键字|关键字|关键字|
|:-----:|:----:|:----:|:----:|
|abstract|assert|boolean|break|
|byte|case|catch|char|
|class|const|continue|default|
|do|double|else|enum|
|extends|final|fianlly|float|
|for|goto|if|implements|
|import|instanceof|int|interface|
|long|native|new|package|
|private|protected|public|return|
|short|static|strictfp|super|
|switch|synchronized|this|that|
|throw|transient|throws|try|
|void|volatile|while|

### Java修饰符

1. **访问修饰符**：default，public，protected，private
2. **非访问修饰符**：final，abstract，strictfp

### Java变量 

1. 本地变量
1. 类变量
1. 实例变量

### Java中的注释

1. 单行注释: //
2. 多行注释: /**/

### Java的对象和类

Java是一种面向对象的语言。
Java包括以下几项基本概念：

1. 封装
1. 继承
1. 多态
1. 抽象
1. 类
2. 对象
1. 实例
2. 消息解析

### Java基本数据类型

变量就是用来存储值而保留的内存位置，这就意味着当你创建一个变量时就会在内存中占用一定的空间。

基于变量的数据类型，操作系统会进行内存分配并且决定什么将被存储在保留内存中。因此，通过给变量分配不同的数据类型，你可以在这些变量中存储整数，小数，或者字母。

Java中有两种有效的数据类型：

1. 原始数据类型
2. 引用数据类型

#### 原始数据类型

byte，short，int，long，float，double，boolean，char。


#### 引用数据类型

引用数据类型是由类的编辑器定义的，它们是用于访问对象的。

### Java常量

常量是代表固定值的源代码。它们直接以代码的形式代表而没有任何估计。

### java变量类型

Java语言支持的变量类型有：

1. 类变量：独立于方法之外的变量，用 static 修饰。
1. 实例变量：独立于方法之外的变量，不过没有 static 修饰。
1. 局部变量：类的方法中的变量。

#### Java 局部变量

1. 局部变量声明在方法、构造方法或者语句块中；
1. 局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁；
1. 访问修饰符不能用于局部变量；
1. 局部变量只在声明它的方法、构造方法或者语句块中可见；
1. 局部变量是在栈上分配的。
1. 局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用。

#### 实例变量

1. 实例变量声明在一个类中，但在方法、构造方法和语句块之外；
1. 当一个对象被实例化之后，每个实例变量的值就跟着确定；
1. 实例变量在对象创建的时候创建，在对象被销毁的时候销毁；
1. 实例变量的值应该至少被一个方法、构造方法或者语句块引用，使得外部能够通过这些方式获取实例变量信息；
1. 实例变量可以声明在使用前或者使用后；
1. 访问修饰符可以修饰实例变量；
1. 实例变量对于类中的方法、构造方法或者语句块是可见的。一般情况下应该把实例变量设为私有。通过使用访问修饰符可以使实例变量对子类可见；
1. 实例变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null。变量的值可以在声明时指定，也可以在构造方法中指定；
1. 实例变量可以直接通过变量名访问。但在静态方法以及其他类中，就应该使用完全限定名：ObejectReference.VariableName。

#### 类变量（静态变量）
1. 类变量也称为静态变量，在类中以static关键字声明，但必须在方法构造方法和语句块之外。
1. 无论一个类创建了多少个对象，类只拥有类变量的一份拷贝。
1. 静态变量除了被声明为常量外很少使用。常量是指声明为public/private，final和static类型的变量。常量初始化后不可改变。
1. 静态变量储存在静态存储区。经常被声明为常量，很少单独使用static声明变量。
1. 静态变量在程序开始时创建，在程序结束时销毁。
与实例变量具有相似的可见性。但为了对类的使用者可见，大多数静态变量声明为public类型。
1. 默认值和实例变量相似。数值型变量默认值是0，布尔型默认值是false，引用类型默认值是null。变量的值可以在声明的时候指定，也可以在构造方法中指定。此外，静态变量还可以在静态语句块中初始化。
1. 静态变量可以通过：ClassName.VariableName的方式访问。
1. 类变量被声明为public static final类型时，类变量名称一般建议使用大写字母。如果静态变量不是public和final类型，其命名方式与实例变量以及局部变量的命名方式一致。

### 访问控制修饰符

Java中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。Javav支持 4 种不同的访问权限。

1. **default** (即缺省，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
2. **private** : 在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）
3. **public** : 对所有类可见。使用对象：类、接口、变量、方法
4. **protected** : 对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类）。

#### 访问控制和继承

请注意以下方法继承的规则：

1. 父类中声明为 public 的方法在子类中也必须为 public。
1. 父类中声明为 protected 的方法在子类中要么声明为 protected，要么声明为 public，不能声明为 private。
1. 父类中声明为 private 的方法，不能够被继承。


### 非访问修饰符
为了实现一些其他的功能，Java 也提供了许多非访问修饰符。

1. **static** 修饰符，用来修饰类方法和类变量。
1. **final** 修饰符，用来修饰类、方法和变量，final 修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的。
1. **abstract** 修饰符，用来创建抽象类和抽象方法。
1. **synchronized** 和 **volatile** 修饰符，主要用于线程的编程。

### Java运算符

计算机的最基本用途之一就是执行数学运算，作为一门计算机语言，Java也提供了一套丰富的运算符来操纵变量。我们可以把运算符分成以下几组：

1. **算术运算符**
2. **关系运算符**
1. **位运算符**
1. **逻辑运算符**
1. **赋值运算符**
1. **其他运算符**

### Java分支结构

if...else/switch语句

### Java循环结构

for/while/do...whild语句

break/continue/goto(是关键字，但不能使用)语句