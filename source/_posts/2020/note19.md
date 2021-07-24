---
title: java 序列化
date: 2017-07-17 17:14:02
categories:
- Java 
tags:
- Java
- 序列化
---

### 一个类必须满足两个条件，它的对象才可以序列化。

1. 必须实现 java.io.Serializable 接口。
2. 该类的所有属性必须是可序列化的

transient 声明的属性不会被序列化。

<!-- more -->

### 创建可以序列化的类

``` java
package com.ccyag;

public class Employee implements java.io.Serializable {

	public String firstName;
	public String lastName;
	public transient int age;
	public String email;
	public String phone;

	public void emailCheck() {
		System.out.println("email:" + email);
	}
}

```

### 序列化对象

``` java

package com.ccyag;

import java.io.*;

public class SerializeDemo {

	public static void main(String[] args) {
		
		Employee e = new Employee();
		e.firstName = "chen";
		e.lastName = "chy";
		e.age = 26;
		e.email = "123@qq.com";
		e.phone = "12345678909";
		
		try {
			FileOutputStream fileOut = new FileOutputStream("/tmp/employee.ser");
			ObjectOutputStream out = new ObjectOutputStream(fileOut);
	        out.writeObject(e);
	        out.close();
	        fileOut.close();
	        System.out.printf("Serialized data is saved succeed.");
		} catch (IOException i) {
			i.printStackTrace();
		}
	}
}

```

### 反序列化对象
``` java
package com.ccyag;

import java.io.*;

public class DeserializeDemo {

	public static void main(String[] args) {
		
		Employee e = null;
	    
		try{
	         FileInputStream fileIn = new FileInputStream("/tmp/employee.ser");
	         ObjectInputStream in = new ObjectInputStream(fileIn);
	         e = (Employee) in.readObject();
	         in.close();
	         fileIn.close();
	      }catch(IOException i)
	      {
	         i.printStackTrace();
	         return;
	      }catch(ClassNotFoundException c)
	      {
	         System.out.println("Employee class not found");
	         c.printStackTrace();
	         return;
	      }
	      System.out.println("Deserialized Employee...");
	      System.out.println("FirstName: " + e.firstName);
	      System.out.println("LastName: " + e.lastName);
	      System.out.println("Age: " + e.age);
	      System.out.println("Email: " + e.email);
	      System.out.println("Phone: " + e.phone);
	      e.emailCheck();
	}
}
```

显示结果：

``` bash
Deserialized Employee...
FirstName: chen
LastName: chy
Age: 0
Email: 123@qq.com
Phone: 12345678909
email:123@qq.com

```

因为 age 属性是短暂的，该值没有被发送到输出流。所以反序列化后 Employee 对象的 age 属性为 0。
