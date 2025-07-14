---
title: 用Java做一个简单的打字游戏
date: 2018-12-29 20:29:38
tags: 
- Java打字游戏
categories: 
- Java
img:  https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/080.jpg
newimg: false
comments: true
zhailu: Java也是可以做桌面程序的。只不过需要运行在装有JDK的电脑环境上，所以应用不是很广泛，但是用来提高自身的代码逻辑还是可以的！
---
Java也是可以做桌面程序的。只不过需要运行在装有JDK的电脑环境上，所以应用不是很广泛，但是用来提高自身的代码逻辑还是可以的！偶有一天看到金山的打字通，就想起何不做个简单的打字游戏用来练练手。于是就有了下文

那话不多说，我们首先建一个类MyTyping，只有main方法，写上总的思路

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/081.jpg)](javascript:void(0);)

运行main方法就可以看到出现屏幕中心出现一个窗体（大小是300*400）

代码逻辑也就思路里那么多。觉得丑的可以自己优化下，个人觉得没必要

OK，出现后就进行下一步

在同一包下新建MyPanel类。继承Panel类

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/082.jpg)](javascript:void(0);)

此时运行main方法，窗体上出现了  黑色的字母C。

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/083.jpg)](javascript:void(0);)

那接下来，就是要让drawString第一个参数为26个随机字母，第二个参数为不超过300的随机数，第三个参数为不超过400的随机数

改造下：

```
g.drawString(new Character((char)(Math.random()*26+97)).toString().toUpperCase(), (int)(Math.random()*300), (int)(Math.random()*400));
```

随机数不会的可以自己百度去。。

多次点击运行，可以看到已经实现，随机位置，随机字母的效果

OK，再下一步。出现10个随机字母。加个循环即可

```
for (int i = 0; i < 10; i++) {
//1.出现的元素，2.元素的x轴，3.元素的y轴
g.drawString(new Character((char)(Math.random()26+97)).toString().toUpperCase(), (int)(Math.random()300), (int)(Math.random()*400));
}
```

效果：（但是有的字母在边缘看不到，没关系，等全部完成了再来优化）

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/084.jpg)](javascript:void(0);)

已经看到 效果已经有了。但是我们设想的的是 字母需要往下移动，怎么完成呢？

也很简单。用一个容器来储存随机字母，以及它的x轴，y轴

改造如下：通过构造方法来实现随机的实现

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/085.jpg)](javascript:void(0);)

再次运行，效果一样

接下来，实现线程，让它下坠

代码改造如下：实现线程需要实现Runnable接口

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/086.jpg)](javascript:void(0);)

运行之后，字母已经实现下坠效果了

核心已经完成了。接下来，加入：

字母超出窗体。重新生成。run方法改造如下

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/087.jpg)](javascript:void(0);)

运行，效果也出来了

再接下来 加入计数器

代码改造如下：定义全局变量来储存积分

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/088.jpg)](javascript:void(0);)

Paint方法：如果积分小于0，不能进来绘制方法，并且出现 game over 字样

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/089.jpg)](javascript:void(0);)

Run方法：如果积分小于0，线程停止

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/090.jpg)](javascript:void(0);)

再次运行。字母超出窗体的时候会在最上面重新生成随机字母。并且积分会-100，当到0时会出现 game  over字样，线程也停止了

但我们现在也发现了。一开始字母随机的位置不对，它可能随机的y轴为350，那岂不是刚出现就要消失了？怎么给人时间去按呢？简单。把生成随机y轴后面的数值改成50，那么他就只会在0-50之间的高度上出现了

改造构造方法：

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/091.jpg)](javascript:void(0);)

运行后，结果也很OK

接下来 实现键盘录入效果

MyPanel实现 KeyListener接口，并实现相应方法（一共三个）

我们只用其中的keyPressed（键盘按下事件）

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/092.jpg)](javascript:void(0);)

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/093.jpg)](javascript:void(0);)


在main方法中将键盘事件注册进去

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/094.jpg)](javascript:void(0);)

再次运行，控制台会输出你输入的字母

那接下来要做的估计都猜到了。匹配键盘录入的字母，

相同：消除这个字母，并且在最上面重新生成，积分+100

不相同：积分-100

代码改造如下：

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/095.jpg)](javascript:void(0);)

但是运行是不是有问题？只要输错一次。直接游戏结束，这是因为输的字母不在范围内，它会循环-100，10次，所以立马就结束了，所以我们现在再给它加个计数器，以避免循环-100

代码改造如下：

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/096.jpg)](javascript:void(0);)

现在效果OK了，但是又有新问题了，如果有一样的两个字母，它并不一定会消除最下面的，但是我们需要它消除最下面的，刚刚我们加了计数器去实现它的减，那么就再加个计数器实现它的加，当键盘录入匹配时，记录下来y轴，跟原始值或者上一个值比较，如果大于，就覆盖这个计数器为当前Y轴，那么最后循环下来，相同的字母也只会保留Y轴最大的那个

代码改造如下

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/097.jpg)](javascript:void(0);)

重新运行，效果基本就算实现了。

可以加一些小的优化。字体加大，颜色随机。

颜色随机，直接放在MyPanel类里就行

改造代码

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/098.jpg)](javascript:void(0);)

如果这样改造。只要动一下就会变颜色。我们想要的是 一生成就固定，直到消失

那还是用容器吧，跟存储随机字母一样的方法，还是全局变量

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/099.jpg)](javascript:void(0);)

OK，再次运行，完美实现

字体加大：

在drawString方法上面加

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/100.jpg)](javascript:void(0);)

看一下效果图

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/101.jpg)](javascript:void(0);)

还是可以的哈。好了就写到这里吧，核心逻辑代码实现就OK了，再写下去要精通swing了

当然这个问题还是有的

字母重叠。没有关闭按钮。没有再来一盘按钮。没有音效

有兴趣的童鞋 可以自己着手优化下。不过个人觉得没必要。因为做的再好，也得用户装了JDK才能运行，后期可以尝试用易语言 或者C#做下这种小工具。

代码我放在github上，有不明白的需要参考可以去下载

地址: [点我](https://github.com/HFanss/test)