---
title: Java Number & Math 类
date: 2018-01-29 20:56:18
tags:
- Java
categories:
- Java
---

一般地，当需要使用数字的时候，我们通常使用内置数据类型，如： **byte**， **short**， **int**， **long**， **float**， **double**。

然而，在实际开发过程中，我们经常会遇到需要使用对象，而不是内置数据类型的情形。为了解决这个问题，Java 语言为每一个内置数据类型提供了对应的包装类。

<!-- more -->

所有的包装类（ **Integer**、 **Long**、 **Byte**、 **Double**、 **Float**、 **Short**）都是抽象类 **Number** 的子类。

这种由编译器特别支持的包装称为装箱，所以当内置数据类型被当作对象使用的时候，编译器会把内置类型装箱为包装类。相似的，编译器也可以把一个对象拆箱为内置类型。Number 类属于 java.lang 包。

下面是一个使用 Integer 对象的实例：

Test.java 文件代码：

```
public class Test{
 
   public static void main(String args[]){
      Integer x = 5;
      x =  x + 10;
      System.out.println(x); 
   }
}
```

以上实例编译运行结果如下：

```
15
```
当 x 被赋为整型值时，由于x是一个对象，所以编译器要对x进行装箱。然后，为了使x能进行加运算，所以要对x进行拆箱。


## Java Math 类

Java 的 Math 包含了用于执行基本数学运算的属性和方法，如初等指数、对数、平方根和三角函数。

Math 的方法都被定义为 static 形式，通过 Math 类可以在主函数中直接调用。


Test.java 文件代码：

```
public class Test {  
    public static void main (String []args)  
    {  
        System.out.println("90 度的正弦值：" + Math.sin(Math.PI/2));  
        System.out.println("0度的余弦值：" + Math.cos(0));  
        System.out.println("60度的正切值：" + Math.tan(Math.PI/3));  
        System.out.println("1的反正切值： " + Math.atan(1));  
        System.out.println("π/2的角度值：" + Math.toDegrees(Math.PI/2));  
        System.out.println(Math.PI);  
    }  
}
```
以上实例编译运行结果如下：

```
90 度的正弦值：1.0
0度的余弦值：1.0
60度的正切值：1.7320508075688767
1的反正切值： 0.7853981633974483
π/2的角度值：90.0
3.141592653589793
```

### Number & Math 类方法

#### xxxValue()
将 Number 对象转换为xxx数据类型的值并返回。
Test.java 文件

```
public class Test{ 
 
   public static void main(String args[]){
      Integer x = 5;
      // 返回 byte 原生数据类型
      System.out.println( x.byteValue() );
 
      // 返回 double 原生数据类型
      System.out.println(x.doubleValue());
 
      // 返回 long 原生数据类型
      System.out.println( x.longValue() );      
   }
}
```
编译以上程序，输出结果为：

```
5
5.0
5
```

#### compareTo()
将number对象与参数比较。

```
public class Test{ 
   public static void main(String args[]){
      Integer x = 5;
      System.out.println(x.compareTo(3));
      System.out.println(x.compareTo(5));
      System.out.println(x.compareTo(8));            
     }
}
```
编译以上程序，输出结果为：

```
1
0
-1
```

#### equals()
判断number对象是否与参数相等。

```
public class Test{
    public static void main(String args[]){
        Integer x = 5;
        Integer y = 10;
        Integer z =5;
        Short a = 5;

        System.out.println(x.equals(y));  
        System.out.println(x.equals(z)); 
        System.out.println(x.equals(a));
    }
}
```
编译以上程序，输出结果为：

```
false
true
false
```

#### valueOf()
返回一个 Number 对象指定的内置数据类型

```
public class Test{ 
public static void main(String args[]){
        Integer x =Integer.valueOf(9);
        Double c = Double.valueOf(5);
        Float a = Float.valueOf("80");               

        Integer b = Integer.valueOf("444",16);   // 使用 16 进制

        System.out.println(x); 
        System.out.println(c);
        System.out.println(a);
        System.out.println(b);
    }
}
```
编译以上程序，输出结果为：

```
9
5.0
80.0
1092
```

#### toString()
以字符串形式返回值。

```
public class Test{
    public static void main(String args[]){
        Integer x = 5;

        System.out.println(x.toString());  
        System.out.println(Integer.toString(12)); 
    }
}
```
编译以上程序，输出结果为：

```
5
12
```

#### parseInt()
将字符串解析为int类型。

```
public class Test{
    public static void main(String args[]){
        int x =Integer.parseInt("9");
        double c = Double.parseDouble("5");
        int b = Integer.parseInt("444",16);

        System.out.println(x);
        System.out.println(c);
        System.out.println(b);
    }
}
```
编译以上程序，输出结果为：

```
9
5.0
1092
```

#### abs()
返回参数的绝对值。

```
public class Test{ 
    public static void main(String args[]){
        Integer a = -8;
        double d = -100;
        float f = -90;    
                        
        System.out.println(Math.abs(a));
        System.out.println(Math.abs(d));     
        System.out.println(Math.abs(f));    
    }
}
```
编译以上程序，输出结果为：

```
8
100.0
90.0
```

#### ceil()
返回大于等于( >= )给定参数的的最小整数。

```
public class Test{
    public static void main(String args[]){
        double d = 100.675;
        float f = -90;    
 
        System.out.println(Math.ceil(d));
        System.out.println(Math.ceil(f)); 
                     
        System.out.println(Math.floor(d));
        System.out.println(Math.floor(f)); 
    }
}
```
编译以上程序，输出结果为：

```
101.0
-90.0
100.0
-90.0
```

#### floor()
返回小于等于（<=）给定参数的最大整数 。

```
public class Test{
    public static void main(String args[]){
        double d = 100.675;
        float f = -90;

        System.out.println(Math.floor(d));
        System.out.println(Math.floor(f));

        System.out.println(Math.ceil(d));
        System.out.println(Math.ceil(f));
    }
}
```
编译以上程序，输出结果为：

```
100.0
-90.0
101.0
-90.0
```

#### rint()
返回与参数最接近的整数。返回类型为double。

```
public class Test{
    public static void main(String args[]){
        double d = 100.675;
        double e = 100.500;
        double f = 100.200;

        System.out.println(Math.rint(d));
        System.out.println(Math.rint(e)); 
        System.out.println(Math.rint(f)); 
    }
}
```
编译以上程序，输出结果为：

```
101.0
100.0
100.0
```

#### round()
它表示四舍五入，算法为 Math.floor(x+0.5)，即将原来的数字加上 0.5 后再向下取整，所以，Math.round(11.5) 的结果为12，Math.round(-11.5) 的结果为-11。

```
public class Test{
    public static void main(String args[]){
        double d = 100.675;
        double e = 100.500;
        float f = 100;
        float g = 90f;
 
        System.out.println(Math.round(d));
        System.out.println(Math.round(e)); 
        System.out.println(Math.round(f)); 
        System.out.println(Math.round(g)); 
    }
}
```
编译以上程序，输出结果为：

```
101
101
100
90
```

#### min()
返回两个参数中的最小值。

```
public class Test{
    public static void main(String args[]){
        System.out.println(Math.min(12.123, 12.456));      
        System.out.println(Math.min(23.12, 23.0));  
    }
}
```
编译以上程序，输出结果为：

```
12.123
23.0
```

#### max()
返回两个参数中的最大值。

```
public class Test{
    public static void main(String args[]){
        System.out.println(Math.max(12.123, 18.456));      
        System.out.println(Math.max(23.12, 23.0));  
    }
}
```
编译以上程序，输出结果为：

```
18.456
23.12
```

#### exp()
返回自然数底数e的参数次方。

```
public class Test{ 
    public static void main(String args[]){
        double x = 11.635;
        double y = 2.76;

        System.out.printf("e 的值为 %.4f%n", Math.E);
        System.out.printf("exp(%.3f) 为 %.3f%n", x, Math.exp(x));  
    }
}
```
编译以上程序，输出结果为：

```
e 的值为 2.7183
exp(11.635) 为 112983.831
```

#### log()
返回参数的自然数底数的对数值。

```
public class Test{
    public static void main(String args[]){
        double x = 11.635;
        double y = 2.76;

        System.out.printf("e 的值为 %.4f%n", Math.E);
        System.out.printf("log(%.3f) 为 %.3f%n", x, Math.log(x));
    }
}
```
编译以上程序，输出结果为：

```
e 的值为 2.7183
log(11.635) 为 2.454
```

#### pow()
返回第一个参数的第二个参数次方。

```
public class Test{
    public static void main(String args[]){
        double x = 11.635;
        double y = 2.76;

        System.out.printf("e 的值为 %.4f%n", Math.E);
        System.out.printf("pow(%.3f, %.3f) 为 %.3f%n", x, y, Math.pow(x, y));
    }
}
```
编译以上程序，输出结果为：

```
e 的值为 2.7183
pow(11.635, 2.760) 为 874.008
```

#### sqrt()
求参数的算术平方根。

```
public class Test{ 
    public static void main(String args[]){
        double x = 11.635;
        double y = 2.76;

        System.out.printf("e 的值为 %.4f%n", Math.E);
        System.out.printf("sqrt(%.3f) 为 %.3f%n", x, Math.sqrt(x));
    }
}
```
编译以上程序，输出结果为：

```
e 的值为 2.7183
sqrt(11.635) 为 3.411
```

#### sin()
求指定double类型参数的正弦值。

```
public class Test{
    public static void main(String args[]){
    
        double degrees = 45.0;
        double radians = Math.toRadians(degrees);

        System.out.format("pi 的值为 %.4f%n", Math.PI);
        System.out.format("%.1f 度的正弦值为 %.4f%n", degrees, Math.sin(radians));

    }
}
```
编译以上程序，输出结果为：

```
pi 的值为 3.1416
45.0 度的正弦值为 0.7071
```

#### cos()
求指定double类型参数的余弦值。

```
public class Test{ 
    public static void main(String args[]){
    
        double degrees = 45.0;
        double radians = Math.toRadians(degrees);

        System.out.format("pi 的值为 %.4f%n", Math.PI);
        System.out.format("%.1f 度的余弦值为 %.4f%n", degrees, Math.cos(radians));

    }
}
```
编译以上程序，输出结果为：

```
pi 的值为 3.1416
45.0 度的余弦值为 0.7071
```

#### tan()
求指定double类型参数的正切值。

```
public class Test{
    public static void main(String args[]){

        double degrees = 45.0;
        double radians = Math.toRadians(degrees);

        System.out.format("pi 的值为 %.4f%n", Math.PI);
        System.out.format("%.1f 度的正切值是 %.4f%n", degrees, Math.tan(radians));

    }
}
```
编译以上程序，输出结果为：

```
pi 的值为 3.1416
45.0 度的正切值是 1.0000
```

#### asin()
求指定double类型参数的反正弦值。

```
public class Test{ 
    public static void main(String args[]){

        double degrees = 45.0;
        double radians = Math.toRadians(degrees);

        System.out.format("pi 的值为 %.4f%n", Math.PI);
        System.out.format("%.4f 的反正弦值为 %.4f 度 %n", Math.sin(radians), Math.toDegrees(Math.asin(Math.sin(radians))));

    }
}
```
编译以上程序，输出结果为：

```
pi 的值为 3.1416
0.7071 的反正弦值为 45.0000 度 
```

#### acos()
求指定double类型参数的反余弦值。

```
public class Test{
    public static void main(String args[]){

        double degrees = 45.0;
        double radians = Math.toRadians(degrees);

        System.out.format("pi 的值为 %.4f%n", Math.PI);
        System.out.format("%.4f 的反余弦值为 %.4f 度 %n", Math.cos(radians), Math.toDegrees(Math.acos(Math.sin(radians))));

    }
}
```
编译以上程序，输出结果为：

```
pi 的值为 3.1416
0.7071 的反余弦值为 45.0000 度 
```

#### atan()
求指定double类型参数的反正切值。

```
public class Test{ 
    public static void main(String args[]){

        double degrees = 45.0;
        double radians = Math.toRadians(degrees);

        System.out.format("pi 的值为 %.4f%n", Math.PI);
        System.out.format("%.4f 的反正切值 %.4f 度 %n", Math.cos(radians), Math.toDegrees(Math.atan(Math.sin(radians))));

    }
}
```
编译以上程序，输出结果为：

```
pi 的值为 3.1416
0.7071 的反正切值 35.2644 度 
```

#### atan2()
将笛卡尔坐标转换为极坐标，并返回极坐标的角度值。

```
public class Test{ 
    public static void main(String args[]){
        double x = 45.0;
        double y = 30.0;
 
        System.out.println( Math.atan2(x, y) );
    }
}
```
编译以上程序，输出结果为：

```
0.982793723247329
```

#### toDegrees()
将参数转化为角度。

```
public class Test{
    public static void main(String args[]){
        double x = 45.0;
        double y = 30.0;

        System.out.println( Math.toDegrees(x) );
        System.out.println( Math.toDegrees(y) );
    }
}
```
编译以上程序，输出结果为：

```
2578.3100780887044
1718.8733853924698
```

#### toRadians()
将角度转换为弧度。

```
public class Test{
    public static void main(String args[]){
        double x = 45.0;
        double y = 30.0;

        System.out.println( Math.toRadians(x) );
        System.out.println( Math.toRadians(y) );
    }
}
```
编译以上程序，输出结果为：

```
0.7853981633974483
0.5235987755982988
```

#### random()
返回一个随机数。

```
public class Test{
    public static void main(String args[]){
        System.out.println( Math.random() );
        System.out.println( Math.random() );
    }
}
```
编译以上程序，输出结果为：

```
0.7798644168924294
0.9984661760744737
```

#### Math 的 floor,round 和 ceil 方法实例比较

|参数|Math.floor|Math.round|Math.ceil|
|:-------:|:------:|:------:|:------:|
|1.4|	1	|1|	2|
|1.5	|1|	2|	2|
|1.6	|1|	2|	2|
|-1.4|	-2	|-1	|-1|
|-1.5|	-2	|-1	|-1|
|-1.6|	-2|	-2	|-1|

floor,round 和 ceil 实例：

```
public class Main {   
  public static void main(String[] args) {   
    double[] nums = { 1.4, 1.5, 1.6, -1.4, -1.5, -1.6 };   
    for (double num : nums) {   
      test(num);   
    }   
  }   
  
  private static void test(double num) {   
    System.out.println("Math.floor(" + num + ")=" + Math.floor(num));   
    System.out.println("Math.round(" + num + ")=" + Math.round(num));   
    System.out.println("Math.ceil(" + num + ")=" + Math.ceil(num));   
  }   
}
```
以上实例执行输出结果为：

```
Math.floor(1.4)=1.0
Math.round(1.4)=1
Math.ceil(1.4)=2.0
Math.floor(1.5)=1.0
Math.round(1.5)=2
Math.ceil(1.5)=2.0
Math.floor(1.6)=1.0
Math.round(1.6)=2
Math.ceil(1.6)=2.0
Math.floor(-1.4)=-2.0
Math.round(-1.4)=-1
Math.ceil(-1.4)=-1.0
Math.floor(-1.5)=-2.0
Math.round(-1.5)=-1
Math.ceil(-1.5)=-1.0
Math.floor(-1.6)=-2.0
Math.round(-1.6)=-2
Math.ceil(-1.6)=-1.0
```




