---
title: Java(一)Java初级语法
date: 2020-4-20 15:46:17
categories:
- Tech 
- Java
tags: [Java]
mathjax: false
urlname: java_grammar_primary
keywords: [Java, Grammar]
description:
---

{% note info %}

**说明**

+ 本文是在`大二下学期`参照`黑马程序员Java系列课程`教程所做笔记，后并为勘误，如有错误，请谅解

{% endnote %}

#### 运算规则

```java
// 1. byte, char, short 类型数据进行计算时，计算结果自动转换为int型
// 2. 小数常量自动为double类型
public class HelloWrold{
    public static void main(String[] args){
        char A = 'b' - 'a';    //error
        int  B = 'b' - 'a';    //B = 1
        float C = 1.05;        //error
        float D = 1.05F;       //D = 1.05
    }
}

// 2. 若表达式中出现不同的转换类型，则记过自动转换成两者中范围更大的数据类型
// 范围大小排序如下表
public class HelloWorld{
    public static void main(String[] args){
     	double A = 1 - 0.5;     //A = 0.5   
    }
}
```

| 类型     | byte | char | short | int  | long | float | double |
| -------- | ---- | ---- | ----- | ---- | ---- | ----- | ------ |
| 字节大小 | 1    | 2    | 2     | 4    | 8    | 4     | 8      |
| 范围等级 | 1    | 1    | 1     | 2    | 3    | 4     | 5      |





#### 赋值运算符

```java
//值得注意的事，在java中，赋值运算符会将计算的结果强制转换为前面变量的类型
public class HelloWorld{
    public static void main(){
        char B = 'A';
        B += 1;
        System.out.println("A = " + A);    //A = B
    }
}
```







#### 字符串的加法

```java
//字符串可以直接与其它类型的变量进行加法运算
/*具体步骤:
	1. 若计算式两边有字符串，且有其他类型数据，则将其他类型数据转化成相应字符串:
	浮点型     1.05 = "1.05"
	boolean型 true = "true"
	int型     5 = "5"
	2. 将后面字符串接到前面字符串后面
	注: 在进行运算时 严格遵循计算顺序
*/
public class HelloWorld{
    public static void main(String[] args){
        System.out.println("Coldeye" + 2020);       // Coldeye2020
        System.out.println("Coldeye" + 2000 + 20);  // Coldeye200020
        Sytem.out.println(2000 + 20 + "Coldeye");   // 2020Coldeye
        
    }
    
}
```





#### 短路运算符 与 基本逻辑运算符

```java
//短路: && or ||
//基本: &  or  |
/*
	短路运算符若计算左边的结果已经足够输出结果，则不会去进行右边算术表达式的计算
*/
public class HelloWorld{
    public static void main(String[] args){
        int i = 10, j = 20, k =30;
        System.out.println((i++ > 100) && (j++ > 100));
        System.out.println("i = " + i);   // i = 11
        System.out.println("j = " + j);   // j = 20
		System.out.println((j++ > 100) & (k++ > 100))
        System.out.println("j = " + j);   // i = 21
        System.out.println("k = " + k);   // j = 31    
    }
}
```





#### 三元表达式

```java
/*
	基本格式:
		关系表达式 ? 表达式1 : 表达式2;
	运算结果:
		先计算关系表达式的结果
		若关系表达式结果为True: 计算表达式1，且运算结果为表达式1的值
		若关系表达式结果为False: 计算表达式2，且运算结果为表达式2的值
*/
public class HelloWorld{
    public static void main(String[] args){
     int a = 100, b = 200;
     System.out.print( true ? a++ : b++); // 100
     System.out.print("a = " + a);        //a = 101
     System.out.print("b = " + b);        //b = 200
    }
}
```





#### 系统输入

```java
//导包
import java.util.Scanner;

public class HelloWorld{
    public static void main(String[] args){
        Scanner sc = new Scnner(System.in);
        int i = sc.nextInt("请输入i的值");
        System.out.println("i = " + i);
    }
}
```







#### 条件判断语句

```java
// if条件语句

/*
	基本格式:
	if (条件判断语句){
		执行语句1;
		....
	}else if (条件判断语句){
		执行语句2;
		....
	}else if (条件判断语句){
		执行语句3;
		....
	}else{
		执行语句n;
		....
	}
*/
```



```java
// switch条件语句 与 case穿透
/*
	表达式中的值可以是:
		byte, short, int, char, string, 枚举
	基本格式:
	switch(表达式):
		case value 1:
			执行语句1;
			break;
		case value 2:
			执行语句2;
			break;
		....
		default value n+1:
			执行语句n+1;
			[break;]        //最后一个break 可以省去
		
*/

/*
	case穿透:
	switch(表达式):
		case value1:
		case value2:
		case value3:
			执行语句1;
			break;
		case value4:
		case value5:
		case value6:
			执行语句2;
			break;
		....
		default:
			执行语句3;
*/
```



#### 循环条件语句

```java
// for 循环语句
/*
	基本格式:
	for(int i=0; i < 10; i++){
		循环体语句;
	}
*/
```



```java
// while 循环语句
/*
	基本格式:
	while (循环判断语句){
		循环体语句;
		循环控制语句;
	}
*/
```



```java
// do while 循环语句
/*
	基本格式:
	do{
		循环体语句;
		循环控制语句;
	}while(循环判断语句);
*/
```

##### 循环跳转语句

```java
break;
continue;
```









#### 内容辅助键与快捷键

```java
//自动生成mian()方法
psvm + enter
//自动生成输出语句
sout + enter
//内容辅助键
Ctrl + Shift + space
    
    
    
//快捷键
//单行注释
Ctrl + /
//多行注释
Ctrl + shift + /
//格式化
Ctrl + Alt + l
//快捷键导包
Alt + Enter
```





#### 数组

```java
//定义数组

//定义数组 以及 其动态初始化
//1.定义了一个int类型数组，数组名是arr_name(最好用这种)
int[] arr_name = new int[size]
//2.定义了一个int类型的变量，变量名是arr_name数组
int arr_name[] = new int[size]
    
//静态初始化
//1.原格式
int[] arr_name = new int[]{数据1, 数据2, 数据3, ...}
//2.简化格式
int[] arr_name = {数据1, 数据2, 数据3, ...}

//两个常见小问题
//1.索引越界
int[] arr = new int[3];
System.out.println(arr[3]);
//空指针异常
int[] arr = new int[3];
System.out.println(arr[0]);
arr = null;
System.out.println(arr[0]);


//数组遍历
//通用格式
int[] arr = {......};
for(int x=0; x<arr.length; x++){
	System.out.println(arr[x]);
}
//其中arr.length可以读取出arr数组的长度
```



#### 方法定义与调用

```java
//定义
public static void method_name(数据类型 参数名称){
    //独立功能代码块
}
```



#### 方法重载

```java
/*
	方法重载:
		多个方法在一个类中
		多个方法具有相同的方法名
		多个方法的参数不相同，类型不同或者数量不同
*/

/*
	方法重载的意义:
		1.使函数可以兼容不同类型的参数，和不同个数的参数
		2.进阶:通过输入的参数种类和个数来控制不同函数(同名不同功能)的调用
*/

public class MethodDemo{
    public static void main(String[] args){
        public static int sum(int a, int b) {
            return a + b;
        }
        public static double sum(double a, double b) {
            return a + b;
        }
        public static double sum(int a, int b, int c) {
            return a + b + c;
        }
        
    }
    //需求1:求两个int类型数据和方法
    
    //需求2:求两个double类型数据和的方法
    
    //需求3:求三个int类型数据和的方法
}
```



#### 传递基本类型/引用类型

```java
/*
	传递基本类型参数原理:
		由于基本类型变量是在栈内存中占据一片空间，用以储存变量名和变量值, 在传递参数时，方法中的形参会在加载到栈内存, 并将被传递变量的值复制过来, 所以改变方法中形参的值不会影响main函数中变量的值
	
	传递引用类型参数原理:
		由于引用类型变量是先在栈内存中占据一块空间, 用以储存变量名并指向一片堆内存空间, 在传递参数时, 方法中的形参会在加载到栈内存，并将被传递变量的值复制过来，由于这次复制过来的是只想堆内存某处的地址信息，所在方法中改变此类型数据的值会改变相对应的堆内存中变量的值，从而影响到main函数中变量所指向堆内存空间的值(即变量的值)
*/
```





## 面向对象

### 调用类与创建对象

```java
/*
	基本格式
		先导入包(若包在同目录下，则无需导包)
		类名  对象名 = new 类名();
	//Example:(创建具有phone类属性与方法的对象p)
		Phone p = new phone
*/
```

### 多对象指向相同

```java
public class StudentTest03 {
	public static void main (String[] args){
		Student s1 = new Student();
		s1.age = "coldeye";
		s1.age = 30;
		System.out.println(s1.name + "," + s1.age);
		Student s2 = new Student();
		s1.age = "haha"
		s2.age = 28
		System.out.println(s1.name + "," + s1.age);
		System.out.println(s2.name + "," + s2.age);
	}
}


/*
	由于对象本身的值是一个指向堆内存某处的地址, 当多个对象指向相同的堆内存时，它们操作的其实是同一片内存中的数据
*/
```

### 成员变量与局部变量

| 区别           | 成员变量                           | 局部变量                                       |
| -------------- | ---------------------------------- | ---------------------------------------------- |
| 类中位置不同   | 类中方法外                         | 方法内或者方法声明中                           |
| 内存中位置不同 | 堆内存                             | 栈内存                                         |
| 生命周期不同   | 随对象存在而存在，随对象消失而消失 | 随方法调用而存在，随方法调用完毕而消失         |
| 初始化值不同   | 有默认的初始化值                   | 没有默认的初始化值，必须先定义，赋值，才能使用 |

### 封装

#### private

```java
//private 可以使变量仅能被同类下的方法所访问和修改，其他类无权访问和修改 
    
public class Student {
	//
    private String name;
    private int age;
    
    //提供get/set方法
    public void setAge(int num) {
        if(a < 0) {
            System.out.println("你输入年龄错误");
        }
        else
            age = num;
    }
    public int getAge() {
        return age;
    }
}
```

#### this

```java
//Java中的this 和 Python中的self相似, this用以在方法中使用'调用该方法的对象的'成员变量(并区别于函数内同名的局部变量)

public class Student {
    private String name;
    private int age;
    
    public void setName(String name) {
        //需要加上this 这个关键字以区分成员变量和局部变量
        this.name = name;
    }
    
    public String getName() {
        //无需加上this 因为没有局部变量
        return name;
    }
    
    public void setAge(int age) {
        this.age = age;
    }
    
    public int getAge() {
        return age; 
    }
}
```

#### 封装

> 面向对象三大特征: 封装, 继承, 多态
>
> 封装的原则:
> 		将类的某些信息隐藏在类内部, 不允许外部程序直接访问，而是通过该类提供的方法来实现对隐藏信息的操作与访问。
>
> 封装的优势:
>
> ​	1.通过方法来控制成员变量的操作，提高了代码的安全性	
> ​	2.把代码进行封装提高了代码的复用性

```java
/*
	构造方法: 
		类比于Python中的 __init__方法
*/
//构造方法是什么?
Scanner sc = new Scanner(System.in);
//这是最早接触的 使用带参数的构造方法的例子, 其中Scanner()被称为构造方法, System.in是传进去的参数, 用以对创建的对象sc进行初始化, 值得注意的是构造方法的方法名需要与类名相同.

public class Student {
    private int age;
    private String name;

    //------------定义一个带参数的构造方法--------------
    public Student(int age, String name) {
        this.age = age;
        this.name = name;
        System.out.println("赋值初始化完成");
    }
    //------------重载一个不带参数的构造方法------------
    public Student() {
        this.age = 18;
        this.name = "Lihua";
        System.out.println("默认初始化完成");
    }

    public void showInfo() {
        System.out.println(name + "," + age);
    }
}

//值得注意的是, 如果你并没有再类中定义一个构造方法, 系统会默认在该类中定义一个无参的构造方法, 而你一旦定义了一个构造方法, 则系统不会再自动定义一个无参的构造方法.
/*
	所以当你定义了一个带参数的构造方法, 下次创建对象是则需要相应的参数，否则会报错，除非
	1. 你定义的参数是默认参数(貌似java并不支持默认参数)
	2. 你使用重载的方法定义了另外一个不带参数的构造方法
*/
```

#### 标准类的制作

1. 成员变量
   + 使用private 修饰成员变量
2. 构造方法
   + 提供一个无参构造方法
   + 提供一个带参构造方法
3. 成员方法
   + 提供每一个成员变量对应的setXxx()/getXxx()
   + 提供一个显示对象信息的show()
4. 创建对象并为其成员变量赋值的两种方式
   + 无参构造方法创建对象后使用setXxx()赋值
   + 使用带参构造方法直接创建带有属性值的对象















#### Java API

> [中文API](https://www.matools.com/api/java8)

> [英文API](https://docs.oracle.com/javase/7/docs/api/)

```java
import java.util.Scanner;

public class HelloWorld {
    public static void main(String[] args) {
        //先写构造方法, 再敲击Ctrl+Alt+V, 自动补全前面创建对象部分
        Scanner scanner = new Scanner(System.in);
        System.out.println("请输入一串字符: ");
        //先调用方法, 再敲击Ctrl+Alt+V, 自动补全前面部分
        String line = scanner.nextLine();
        System.out.println("您输入的字符串为: " + line);

    }
}
```

























### String 

#### 概述

​		String类在`java.lang` 包下, 所以使用的时候不需要导包。
​		String类代表字符串，Java程序中的所有字符串文字(例如"abc") 都被实现为此类的实例, 也就是说, Java程序中的所有双引号字符串都是String类的对象

--------------------------

#### 字符串的特点

+ 字符串不可变，他们的值在创建后不能被更改
+ 虽然String的值是不可变的，但是他们可以被共享
+ 字符串的效果上相当于字符数组(char[]), 但是底层原理是字节数组(byte[])

------------------------------

#### String类对象的创建

```java
// 构造方法的方式
// 1. 无参构造方法:创建一个空白字符串对象, 不含有任何内容
public String = new String();

// 2. 字符数组参数构造方法:根据字符数组内容创建字符串对象
char[] chs = {'F', 'u', 'c', 'k', ' ', 'Y', 'o', 'u', ',', 'B', 'i', 't', 'c', 'h'};
public String = new String(chs);

// 3. 字节数组参数构造方法:根据字节数组内容创建字符串对象
byte[] bys = { (各个字符所对应的ASCII码) }
public String = new String(bys);



// 直接赋值的方式
// 4. 字节赋值创建字符串对象
public String = "Fuck You, Bitch"
```

--------------------------------

#### 不同方式创建String类对象的区别

```java
/*
	1. 构造方法创建的对象的特点
		由于, 该类方法每次创建一次对象都会使用一次 'new' 来申请一个内存空间, 故虽然内容相同, 但是地址值不同 
*/
// 如下, s1 和 s2 创建对象时所参考的对象相同(都是字符数组chs) 但 他们的地址不同(即s1 和 s2 指向的不是同一个对象).
char[] chs = {'a', 'b', 'c'};
String s1 = new String(chs);
String s2 = new String(chs);


/*
	2. 直接赋值创建的对象的特点
		以" "方式给出的字符串, 只要字符串序列相同(顺序和大小写), 无论在程序中出现多少次, JVM都只会建立一个String对象, 并在字符串池中维护
*/
// 如下, JVM首先会创建一个String对象放在字符串池中, 并给s3参考; 然后再创建s4时, 则直接让其指向字符串池中上一步已经创建好的String对象，也就是说本质上他们是同一个对象
String s3 = 'abc';
String s4 = 'abc';
```

```java
//测试代码
public static void main(String[] args) {
    //构造方法得到
    char[] chs = {'a', 'b', 'c'};
    String s1 = new String(chs);
    String s2 = new String(chs);
    System.out.println(s1 == s2);
    
    //直接赋值得到
    String s3 = "abc";
    String s4 = "abc";
    System.out.println(s3 = s4);
    
}
```

![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20200729125326551.png)

---------------------------------

#### String类的常见方法使用

| 方法                     | 作用                         | 返回值                           |
| ------------------------ | ---------------------------- | -------------------------------- |
| str1.equals(String str2) | 判断两个字符串中内容是否一致 | Boolean  相同为True, 不同为False |
| str1.charAt(int index)   | 输出索引处字符的char值       | char 返回索引处字符的char值      |
|                          |                              |                                  |



##### 字符串的比较

```java
//利用 == 判断是否指向的是同一个字符串对象(指向地址时候一样)

//利用 equals() 判断字符串内容是否一样
public static void main(String[] args) {
    char[] chs = {'a', 'b', 'c'};
    String s1 = new String(chs);
    String s2 = new String(chs);
    
    String s3 = "abc";
    String s4 = "bcd";
    System.out.println(s1.equals(s2));
    System.out.println(s2.equals(s3));
    System.out.println(s3.equals(s4));
}
```

##### 字符串的遍历

```java
// 1. 返回字符串中指定索引处的char值, 字符串public char charAt(int index)
// 2. 利用for循环遍历字符串

//通用格式
for (int i = 0; i < s.length(); i++) {
    System.out.println(s.charAt(i));	//就是索引处的字符值
}
```

##### 统计字符次数

```java
public static void main(String[] args) {
        int smallCount = 0;
        int bigCount = 0;
        int numberCount = 0;
        System.out.println("请输入字符串");
        Scanner scanner = new Scanner(System.in);
        String line = scanner.nextLine();
        for (int i = 0; i < line.length(); i++) {
            char ch = line.charAt(i);
            if (ch >= 'A' && ch <= 'Z') {
                bigCount++;
            } else if (ch >= 'a' && ch < 'z') {
                smallCount++;
            } else if (ch >= '0' && ch < '9') {
                numberCount++;
            }
        }
        System.out.println("大写字母有" + bigCount + "个");
        System.out.println("小写字母有"+ smallCount + "个");
        System.out.println("数字有"+ numberCount + "个");
}
```













### String Builder

#### 背景

##### 		String类的对象进行拼接操作时在内存中的情况:

```java
public static void main(String[] args) {
    String s = "hello";
    s += "world";
    System.out.println(s);
}
```

![](https://picgo-1301748200.cos.ap-chengdu.myqcloud.com/image-20200729143509091.png)

> ​	如图中所示, 对于第2行代码, 首先在堆内存的String常量池中创建了字符串常量"hello", 地址为001(假设), 再在栈内存的main方法中创建了一个String类对象s, 指向地址001(假设).
> ​	 执行第3行代码时, 因为 "hello" 为字符串常量不可以修改, 所以首先在堆内存的String常量池中创建了堆内存"world", 地址为002(假设), 由于是拼接操作, String类对象s只能指向一个地址, 但是常量池中并没有一个内容为"helloworld"常量, 所以会在堆内存中再创建一个"helloworld"字符串常量, 地址为003, 并将栈内存中的s指向003.

##### 		String拼接原理带来的坏处

​		很明显, 如果对字符串进行拼接操作, 每次拼接, 都会构建一个新的String对象, 且保留之前已经创建的String对象, 既耗时, 又浪费内存空间, 而且这种操作还无可避免. 所以我们需要引入一种新的类来解决这个问题, 这个类就是StringBuilder类.

#### StringBuilder 概述

​		StringBuilder 是一个可变的字符串类, 我们可以把它看成是一个容器, 这里的可变指的是StringBuilder对象中的内容是可变的

String 和 StringBuilder的区别:

+ String:内容是不可变得
+ StringBuilder:内容是可变的

#### StringBuilder 构造方法

```java
/*
	方法1: public StringBuilder(), 创建一个空白的可变的字符串对象，不含有任何内容
	方法2: public StringBuilder(String str), 根据字符串的内容, 来创建可变字符串对象
*/


public class HelloWorld {
    public static void main(String[] args) { 
        StringBuilder sb = new StringBuilder();
        System.out.println("sb" + sb);
        System.out.println("sb.length()" + sb.length());
        
        StringBuilder sb2 = new StringBuilder("HelloWorld");
        System.out.println("sb2" + sb2);
        System.out.println("sb2.length()" + sb2.length());
    }
}
```

#### StringBuilder类的常见方法使用

| 方法                     | 作用                              | 返回值                                     |
| ------------------------ | --------------------------------- | ------------------------------------------ |
| sb1.append(任意类型数据) | 在sb1后添加数据, 并返回对象自身   | StringBuilder       返回添加数据后对象本身 |
| sb1.reverse()            | 将sb1的内容进行反转, 返回对象本身 | StringBuilder        返回反转后对象本身    |



```java
public class HelloWorld {
    public static void main(String[] args) { 
        StringBuilder sb = new StringBuilder();
       	//调用append()方法, 并将返回值赋值给sb2
        StringBuilder sb2 = sb.append("hello");
        //查看sb, sb2内容
       	System.out.println("sb: " + sb);
        System.out.println("sb2: " + sb2); 
        
        //链式编程原理:
        //1. 对象.对象具有的方法 返回 对象
        //2. (对象.对象具有的方法).对象具有的方法
        StringBuilder sb3 = new StringBuilder();
        sb3.append("Hello").append("world").append("java").append(100);
        //查看sb3的内容
        System.out.println("sb3: " + sb3);       
    }
}
```

#### String与StringBuilder的相互转换

| 方法                    | 作用                                         | 返回值 |
| ----------------------- | -------------------------------------------- | ------ |
| sb1.toString()          | 根据StringBuilder类对象sb1内容返回一个String | String |
| StringBuilder(String s) | 通过构造方法把String转换为StringBuilder类    |        |

```java
public static void main(String[] args) {
    StringBuilder sb = new StringBuilder("Hello, World");
    sb.append(" world~~");
    //sb本身不会转换为String, 而是返回一个内容相同的String
    String str = sb.toString();
    	
    
    //利用构造方法创建与String类对象str2内容相同的StringBuilder类对象sb2
   	String str2 = "Fuck";
    StringBuilder sb2 = new StringBuilder(str2);
}
```

