---
title: 对list中对象的某一属性排序
date: 2019-01-18 20:29:38
tags: 
- Java
categories: 
- 学习记录
img: https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/007.png 
newimg: false
comments: true
zhailu: 针对list集合中的单个元素活对象元素进行排序，分为单个元素与对象元素的排序
---
如果list只包含string的话，排序其实很方便

```
@Test
    public void test003() {
        List<String>  list = new ArrayList<String>();
        list.add("3");
        list.add("1");
        list.add("5");
        list.add("6");
        System.err.println("排序前："+list);
        //第一种方式
        Collections.sort(list);
        System.err.println("排序后："+list);
        //第二种方式
        /**
        Collections.sort(list, new Comparator<String>() {
            
            @Override
            public int compare(String o1, String o2) {
                // TODO Auto-generated method stub
                return o1.compareTo(o2);
            }
        
        });
        */
    }
```

> 控制台

```
第一种方式和第二种方式输出相同：
排序前：[3, 1, 5, 6]
排序后：[1, 3, 5, 6]
```

两种方式其实底层实现了同样的方法，不同的只是一个复写了compare方法

这是默认升序，那么降序呢？只需要修改下compare方法即可

```
Collections.sort(list, new Comparator<String>() {
            
            @Override
            public int compare(String o1, String o2) {
                // TODO Auto-generated method stub
                return o2.compareTo(o1);
            }
        
        });
```

> 那么对于对象集合，怎么排序呢？

```
@Test
    public void test003() {
        List<User>  list = new ArrayList<User>(4);
        User u1 = new User("张三", 17, "20181212");
        User u2 = new User("李四", 2, "20171105");
        User u3 = new User("王五", 11, "19950504");
        User u4 = new User("李六", 5, "20200406");
        list.add(u1);
        list.add(u2);
        list.add(u3);
        list.add(u4);
        System.err.println("排序前：");
        for (User user : list) {
            System.err.println(user);
        }
        Collections.sort(list, new Comparator<User>() {

            @Override
            public int compare(User o1, User o2) {
                return o1.getCreateTime().compareTo(o2.getCreateTime());
            }
            
        
        });
        System.err.println("排序后：");
        for (User user : list) {
            System.err.println(user);
        }
    }
```

> 控制台

```
排序前：
User [user=张三, age=17, createTime=20181212]
User [user=李四, age=2, createTime=20171105]
User [user=王五, age=11, createTime=19950504]
User [user=李六, age=5, createTime=20200406]
排序后：
User [user=王五, age=11, createTime=19950504]
User [user=李四, age=2, createTime=20171105]
User [user=张三, age=17, createTime=20181212]
User [user=李六, age=5, createTime=20200406]
```

可以看出，不同之处只是在compare方法内把对象中要比较的属性抽出来而已

默认升序，降序的话换下顺序即可,

如果针对属性为Integer的属性的话，方法也是一样