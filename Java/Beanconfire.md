# Beanconfire

### 1. Interview 1

网上海投的icc Beaconfire的Java backend engineer. 因为投的是和Java相关的职位，所以问题一般都是和Java有关. 首先是电话面试，简单了解一下背景，然后就问知不知道OOP, Inheritance是啥, Polymorphism是啥，

过了就约时间网上笔试. 网上笔试时间一个小时，用Skype. 面试官是个华人小哥，首先还是问一下背景和简历，然后就问有没有用过Java相关的framwork, 比如Spring boot 啥的，然后就是一堆关于Java的问题: 

什么是abstract class和interface？ 

什么是final？ 

什么是method ovrriding和method overloading？ 

method overriding 和 method overloading 可不可以用final? 

- private and **final methods can** be **overloaded** but they cannot be **overridden**. It means a class **can** have more than one private/**final methods** of same name but a child class cannot **override** the private/**final methods** of their base class.

abstract class 和 interface可不可以用final? 

什么是hashmap? hashmap 怎么实现？  

然后就是两道简单题，每一道20分钟. 第一题: 给定一个int array，找最长的递增子array的长度, 举个例子: 给定的array num = [1，2，3，4，5，6，7]，那么返回长度是7，因为这整个array都是递增. 给定的array num = [1,2,3,1,5,7,8,9]，返回长度是5，因为最长递增子array是[1,5,7,8,9]。 

第二题: 给定两个String s1 和 s2, 但是s2里面可能会有s1里面重复的字母，要求看看这两个String 是不是相等, 要返回true或者false 举个例子: 给定两个Strinng s1 = "alex", String s2 = "aalleex", 要返回true, 因为s2字母个数可以重复，但是字母的顺序是正确的，所以返回true. 给定的两个String s1 = "laiden", String s2 = "liaden"，要返回false，虽然s2字母和个数都一样，但是顺序不正确，所以false.  两道题都可以假设输入不为空，不为null，都要分析时间和空间复杂度. 题的话是面试官发给你，没有用hackerrank，没有test case 和 其他写好的function, 因为用Java, 就一个main method, 其他自己写.    

**补充内容 (2020-11-3 04:37):** 今天最后一轮 behavioral questions interview, 30 分钟，和VP 用Skype 聊. VP 也是个华人小哥. 基本上也是先介绍自己，然后介绍一下自己做过的项目，然后就问了两个behavioral questions.  **补充内容 (2020-11-3 04:40):** 

问题1: 如果项目是这个月底截止，但是你知道你在下个月底之前你是做不出来了，你会怎么办？ 

问题2: 如果派你到一个公司，没有任何trainning，guidance，和其他任何帮助，但是需要你有某些技能，一个月时间你会怎办？



https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=680458&highlight=beaconfire



### 2. Interview 2

Interview Questions

1. polymorphism?

   Polymorphism: It's a characteristic of being able to assign a different meaning or usage to something in different contexts.

   There are two types of polymorphism in Java: compile-time polymorphism and runtime polymorphism. We can perform polymorphism in java by method overloading and method overriding.

2. inheritance?

   It is the mechanism in java by which one class is allow to inherit the features(fields and methods) of another class.

3. overwrite vs overload.

![method overriding and method overloading](C:\Users\betti\Desktop\Leetcode-questions\Java\method overriding and method overloading.png)

4. what is OOP?  

   As the name suggests, Object-Oriented Programming or OOPs refers to languages that use objects in programming. Object-oriented programming aims to implement real-world entities like inheritance, hiding, polymorphism etc in programming. The main aim of OOP is to bind together the data and the functions that operate on them so that no other part of the code can access this data except that function.

   There are FOUR main concepts of OOP in Java: abstraction, encapsulation, inheritance and polymorphism

5. What is final and static?

   **final** keyword implies something, which cannot be changed. For example - **final** variables cannot be reassigned, **final** fields in a class cannot be set once they’re defined, **final** methods cannot be overridden, and, **final** classes cannot be extended/subclassed. 

   **static** keyword in Java and C++ have the same meaning. **static** denotes a property, which is shared by all objects/instances of a class and does not vary from one instance to another. This also means, that you do not need an instance to get access to **static** members, they can be accessed via the class itself. 

6. Abstract class and Interface

   Data Abstraction is the property by virtue of which only the essential details are displayed to the user. The trivial or the non-essentials units are not displayed to the user. Ex: A car is viewed as a car rather than its individual components.

   In java, abstraction is achieved by [interfaces](https://www.geeksforgeeks.org/interfaces-in-java/) and [abstract classes](https://www.geeksforgeeks.org/abstract-classes-in-java/). We can achieve 100% abstraction using interfaces.

### 3. Interview 3

what is polymorphism?
what is interface?
what is final and static?  

Whats difference between abstract class and interface.  



