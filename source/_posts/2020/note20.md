---
title: Java 继承
date: 2017-07-07 11:02:33
categories:
- Java
tags:
- Java
- 继承
---

### 继承的概念
>继承是java面向对象编程技术的一块基石，因为它允许创建分等级层次的类。
继承就是子类继承父类的特征和行为，使得子类对象（实例）具有父类的实例域和方法，或子类从父类继承方法，使得子类具有父类相同的行为。
<!-- more -->

### 创建父类 Animal.java

```java

public class Animal {

	//私有属性
	private String name;
	private int age;
	
	//存取方法
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	
	// 构造函数
	public Animal(String name, int age) {
		this.name = name;
		this.age = age;
	}
	
	//方法
	
	public void eat() {
		System.out.println(name + "正在吃饭。");
	}
	
	public void sleep() {
		System.out.println(name + "正在睡觉。");
	}
	
	public void sayHello() {
		System.out.println("Hello, my name is " + name + ", I'm " + age + " years old.");
	}
	
}


```

### 创建子类 Cat.java and Dog.java

```java
public class Cat extends Animal {

	public Cat(String name, int age) {
		super(name, age);
	}
}
```

```java

public class Dog extends Animal {
	public Dog(String name, int age) {
		super(name, age);
	}
}


```

### 测试类 Test.java

```java
public class Test {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		Dog myDog = new Dog("dog", 2);
		myDog.eat();
		myDog.sleep();
		myDog.sayHello();
		myDog.setAge(3);
		myDog.sayHello();
		Cat myCat = new Cat("cat", 1);
		myCat.eat();
		myCat.sleep();
		myCat.sayHello();
	}

}
```