---
title: ArrayList的源码解析
author: Loky
date: 2020-08-14 21:32:00 +0800
categories: [Java,ArrayList]
tags: [ArrayList,Java]
---

# ArrayList的源码解析

------

1. ## 结构

   是List接口的实现类，而List接口继承Collection接口，同为List接口的实现类还有LinkList类，ArrayList与LinkList不同在于实现结构：

   > ArrayList：数组结构
   >
   > LinkList: 链表结构

2. ## 源码分析

   ArrayList默认容量大小：

   ```java
   private static final int DEFAULT_CAPACITY = 10;//默认容量为10  
   ```

   存放元素的数组：

   ```java
   transient Object[] elementData;
   ```

   实际元素个数：
   
   ```java
   private int size;
   ```
   
   无参构造：
   
   ```java
   public ArrayList() {
       this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
   }//意为，没有添加元素时，容量大小为0
   ```
   
   add方法：
   
   ```java
   public boolean add(E e) {
       ++this.modCount;
       this.add(e, this.elementData, this.size);
       return true;
   }
   ```
   
   ```java
   private void add(E e, Object[] elementData, int s) {
       if (s == elementData.length) {
           elementData = this.grow();
       }
   
       elementData[s] = e;
       this.size = s + 1;
   }
   ```
   
   <!--典型的数组操作-->
   
   扩容操作：
   
   ```java
   private int newCapacity(int minCapacity) {
       int oldCapacity = this.elementData.length;
       int newCapacity = oldCapacity + (oldCapacity >> 1);
       if (newCapacity - minCapacity <= 0) {
           if (this.elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
               return Math.max(10, minCapacity);
           } else if (minCapacity < 0) {
               throw new OutOfMemoryError();
           } else {
               return minCapacity;
           }
       } else {
           return newCapacity - 2147483639 <= 0 ? newCapacity : hugeCapacity(minCapacity);
       }
   }
   ```
   
   ```java
   private Object[] grow() {
       return this.grow(this.size + 1);
   }
   ```
   
   ```java
   private Object[] grow(int minCapacity) {
       return this.elementData = Arrays.copyOf(this.elementData, this.newCapacity(minCapacity));
   }
   ```
   
   