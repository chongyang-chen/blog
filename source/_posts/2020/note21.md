---
title: Java 文件(File)操作
date: 2017-07-07 10:11:45
categories:
- Java
tags:
- Java
- 文件
---

java 文件操作
<!-- more -->

### File文件操作

```java 
File file = new File("/Users/Chen/Desktop/test.txt");
	
FileOutputStream fileOutputStream = new FileOutputStream(file);
	
OutputStreamWriter writer = new OutputStreamWriter(fileOutputStream, "UTF-8");
// 构建OutputStreamWriter对象,参数可以指定编码
    
writer.append("中国");
// 写入到缓冲区
    
writer.append("\r\n");
    
writer.append("English");
// 刷新缓存冲,写入到文件,如果下面已经没有写入的内容了,直接close也会写入
    
writer.close();
//关闭写入流,同时会把缓冲区内容写入文件,所以上面的注释掉
    
fileOutputStream.close();
// 关闭输出流,释放系统资源
    
FileInputStream fileInputStream = new FileInputStream(file);
// 构建FileInputStream对象
    
InputStreamReader reader = new InputStreamReader(fileInputStream, "UTF-8");
// 构建InputStreamReader对象,编码与写入相同
 
StringBuffer stringBuffer = new StringBuffer();
while (reader.ready()) {
	stringBuffer.append((char) reader.read());
	// 转成char加到StringBuffer对象中
}
System.out.println(stringBuffer.toString());
reader.close();
// 关闭读取流
    
fileInputStream.close();
// 关闭输入流,释放系统资源

```

### 创建文件夹

```java

String dirname = "/tmp/chen/java/test";
File d = new File(dirname);
// 现在创建目录
	
if (d.mkdirs()) {
	System.out.print("success");
} else {
	System.out.print("failed");
}


```


### 读取文件目录

```java
String dirname = "/tmp";
File f1 = new File(dirname);
if (f1.isDirectory()) {
	System.out.println( "目录 " + dirname);
	String s[] = f1.list();
	for (int i=0; i < s.length; i++) {
		File f = new File(dirname + "/" + s[i]);
		if (f.isDirectory()) {
			System.out.println(s[i] + " 是一个目录");
		} else {
			System.out.println(s[i] + " 是一个文件");
		}
	}
} else {
	System.out.println(dirname + " 不是一个目录");
}

```

### 删除文件夹

```java

public static void main(String args[]) {
// 这里修改为自己的测试目录
	File folder = new File("/tmp/java/");
	deleteFolder(folder);
}
 
//删除文件及目录
public static void deleteFolder(File folder) {
	File[] files = folder.listFiles();
	if(files!=null) { 
		for(File f: files) {
			if(f.isDirectory()) {
				deleteFolder(f);
			} else {
				f.delete();
			}
		}
	}
	folder.delete();
}


```
