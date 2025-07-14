---
title: Java代码的优化
date: 2018-12-25 20:29:38
tags: 
- Java代码优化
categories: 
- Java
img: https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/030.jpg
newimg: false
comments: true
zhailu: 做java也很久了，自己也积累了一些代码优化方面的心得，一个好的代码是体现程序员水平的最直观体现，下面来看一下代码方面比较常见的优化点
---
做java也很久了，自己也积累了一些代码优化方面的心得，一个好的代码是体现程序员水平的最直观体现，下面来看一下代码方面比较常见的优化点
（本文在书写过程中也参考了一些其他文章，在这里就不一一赘述，内容也比较浅显，忘大神轻喷，如有错误的地方，还请在评论中指出来，我会一一改正）

## 1.减少对变量的重复计算--》for循环的优化

```
 for (int i = 0; i < args.length; i++)   
{   

}   
```

 更改为

```
for (int i = 0,index=args.length; i < index; i++)    
{  
    
}  
```

 原理：每次在i++的时候都会重新计算一次args.length,优化之后只会计算一次  

当然这个也是相对于args很大时，当args不大时，其实效率也差不多，但是我们养成个好习惯总是好的。而且它可以直接修改for循环的模版实现，比较方便 

 修改eclipse的模版：Preferences->java->Editor->Templates找到for修改为上面的内容 

## 2.底层使用可变数组的数据结构尽量指定长度  

例如最常用的ArrayList,HashMap 

```
List list = new ArrayList<>(10);  
 
Map map = new HashMap<>(10); 
```

原理：可变数组都有一个扩容政策，当数据量超过它的加载因子时，就会执行扩容操作
当指定长度时，只有在超过指定的长度时，才会执行扩容操作，所以我们使用的时候应尽量预估它的大小，尽量指定大小

## 3.String类尽量使用StringBuffer、StringBuilder

这个涉及到jvm的内存分配，举个例子

```
String str = “abc”;    String str2 = str + “ccd”;  
```

jvm会在堆内存中开辟3个空间，1为“abc”,2为“ccd”,3为“abcccd”,最终str2指向3，1和2因为没有被引用，会在GC回收机制内被回收，而GC的开销是相当大的，所以应尽量避免
那么使用StringBuffer是什么情况呢

```
StringBuffer str =“abc”;    str.append(“ccd”);  
```

jvm只会在堆空间中开辟一个空间“abc”,执行append时只会在“abc”的空间上+“ccd”
因此避免了GC的回收，也避免了内存的浪费
同样是为了获取到“abcccd”,但第二种方式明显更有效率
那怎么判断是使用StringBuffer还是StringBuilder的呢？
如果有线程安全的考虑使用StringBuffer，无则使用StringBuilder，线程安全也是一个比较高的开销

## 4.使用equals()方法时常量尽量写前面

例如：

```
Brand brand = new Brand();           
brand.setImgUrl("dddddddddd");          
// brand.setName("HFanss");           
String ss = "HFanss";           
if (brand.getName().equals(ss))          
{          
	System.err.println("相同");          
}else{              
	System.err.println("不相同");          
}  
```

抛出空指针异常，应修改为：

```
if (ss.equals(brand.getName())
```

这时候会输出   不相同。
原理：equals的源码解释 当比较对象（常量ss）为空时，抛出空指针异常，
而被比较对象（brand.getName()）为空时,则直接以 false结束

## 5.尽量采用懒加载的策略，就是在需要的时候才创建

如：

```
String str = "HFanss";             
if ("2".equals(status))                
{                    
	list.add(str);                
} 
```

应该为：

```
if ("2".equals(status))            
{                 
    String str = "HFanss";                
    list.add(str);            
}  
```

原理：这个应该很容易看懂的，当if不成立时，创建的字符串就没用了，面临GC回收，应该有效避免，写在if内部

## 6.在数值运算时，遇到偶数乘、除偶数倍时，尽量使用位移运算

如：

```
int a = 2;    
int b = 16;    
System.err.println(a<<5);//等同于  222222   即232    System.err.println(b>>2);//等同于  16/2/2      即16/4  
```

原理：即使使用  2*32、16/4的方式，最终在底层的算法还是位移，因为位移是基于2进制的算法，任何运算都会转换成二进制再运算，那我们直接使用二进制就会提升一部分效率

## 7. 对象引用的优化

如： 

```
List list = new ArrayList<>();          
for (int i = 0; i < 1000; i++)          
{              
    Object obj  = new Object();                 
    list.add(obj);          
}  
```

应该为：

```
List list = new ArrayList<>();          
Object obj = null;          
for (int i = 0; i < 1000; i++)          
{              
    obj  = new Object();                 
    list.add(obj);          
}  
```

原理：我们的目的只是list.add(obj)这一步，
前者obj引用会在栈空间中有1000个，但是最终只会用到1个，
后者obj引用在栈空间只有1个，提升效果不言而喻！

## 8.慎重使用static静态

使用静态后，编译时会直接创建，而且直到程序结束，一般只会用在常量，公共方法上，因为需要保证随时随地使用，基于这一需求，它不太使用于对象的创建上，会浪费内存

## 9.常量的优化

相信这个大家应该都很熟悉，常量名大写 用以和变量区分，而且加上static final修饰，保证使用的速度和不被外界力量所改变

## 10.将变量转换成字符串时尽量使用to.string()方法

一般有3种方法

```
Integer s = 5;    
s.toString();    
String.valueOf(s);//源码显示调用了Integer.toString()方法，而且会在调用前做空判断    s+“”;//源码显示使用StringBuilder实现，先用append方法拼接，再用toString()方法对比而言，直接调用最底层的toString()方法无疑是效率最高的  
```

接下来是一些体系上的优化，分为 结构优化，日志优化，可读性优化，异常优化
结构优化：

```
A. action层尽量不要做参数的校验和逻辑书写，它只负责请求的转发和响应，入参和出参

B. Service层逻辑要清晰，尽量不要有if,for的出现，全部封装到公共方法去调用

C. DAO层只提供持久层相关操作，如封装参数进map供持久层使用，尽量不要有逻辑在里面，所有的逻辑应都在service里完成
```

日志优化：

```
A. 方法开始后、结束前书写日志

B. 抓取异常时书写日志

C. 特殊情况时书写。如需要提前return时
```

可读性优化：

```
A. 类、方法必须要有注释

B. 在一些比较大的逻辑前加上注释

C. 一个完美的service层，应逻辑清晰，一行代码代表一个逻辑，通篇下来可读性非常强
```

异常优化：

```
A. 异常应只用来进行错误处理，而不是逻辑处理（异常也是高开销的操作）

B. 善用多种异常，但是在service层应只有一个 try cath来抓取多个异常，并分别处理

C. 异常理应在service层全部处理完，不能再继续往上抛（理论上可以接续抛，但service本来就是处理逻辑的，尽量在本层处理完）
```

以上是代码优化方面的一些常见点，当然这并不是全部，一个完美的代码是有很多优化点的，而且代码优化方面也不止这些，本人只是基于自己的经验给新来的同志一些借鉴之处。
除了代码优化，还有一些容器优化，项目优化，网络优化，缓存优化等等，编程是一个枯燥的过程，望共勉之！
最后给大家安利一个好用的插件--》阿里巴巴代码规范检测插件
[![2018061017121995.png](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/031.jpg)](javascript:void(0);)
红框内的就是执行检测后提示的信息，会提示不符合阿里巴巴规范的代码
安装使用教程 ： [点我](https://blog.csdn.net/lx_nhs/article/details/79099582)