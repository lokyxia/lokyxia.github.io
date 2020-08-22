---
title: 关于Collection接口中的遍历方法
author: Loky
date: 2020-08-15 12:09:00 +0800
categories: [Java,Collection]
tags: [Collection,Java]
---

# 关于Collection接口中的遍历方法

------

1. ## 使用增强for循环

   ```java
   import java.util.ArrayList;
   import java.util.Collection;
   
   
   public class demo1 {
       public static void main(String[] args) {
           Collection collection = new ArrayList();
           //添加add
           collection.add("1");
           collection.add("2");
           collection.add("3");
           System.out.println(collection.size());//3
           System.out.println(collection.toString());//[1, 2, 3]
           System.out.println(collection);//[1, 2, 3]
   		//遍历
   		// 1.使用增强for
           for (Object object: collection) {
               System.out.println(object);
           }
           
       }
   ```

   > 这里打印2遍是比较，调用toString和直接打印的区别ArrayList的toString 方法被重写了，和直接打印输出一样
   
2. ## 使用迭代器

   ```java
   package Collection体系;
   
   import java.util.ArrayList;
   import java.util.Collection;
   import java.util.Iterator;
   
   public class demo1 {
       public static void main(String[] args) {
           Collection collection = new ArrayList();
           //添加add
           collection.add("1");
           collection.add("2");
           collection.add("3");
           //2.使用迭代器(迭代器专门用来遍历集合的一种方式)
   //          步骤：1.hasnext();
   //               2.next();
   //               3.remove();
           Iterator it = collection.iterator();
           while (it.hasNext()){
               Object ob = it.next();
               System.out.println(ob);
   //   collection.remove(ob);//不能使用Collection的删除方法
               it.remove();
           }
       	}
       }
           
   ```
