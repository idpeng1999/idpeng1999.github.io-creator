---
title: "IOC"
date: 2022-04-04T22:14:33+08:00
draft: false
categories: [java知识]
---
控制反转（Inversion of Control，简称IoC）

是面向对象编程中的一种设计原则，可以用来减低计算机代码之间的耦合度。

* 其中最常见的方式叫做`依赖注入`（Dependency Injection，简称DI）；（ Spring 使用的方式，`容器负责组件的装配`）
* 还有一种方式叫`依赖查找`（Dependency Lookup）。（已经`被抛弃`）
* 通过控制反转，对象在被创建的时候，由一个调控系统内所有对象的外界实体，将其所依赖的对象的引用传递(注入)给它。


## IOC容器的原理

IOC容器其实就是一个大工厂，它用来管理我们所有的对象以及依赖关系。

* 原理就是通过Java的反射技术来实现的！通过反射我们可以获取类的所有信息(成员变量、类名等等等)！ 
* 再通过配置文件(xml)或者注解来描述类与类之间的关系 
* 我们就可以通过这些配置信息和反射技术来构建出对应的对象和依赖关系了！

## Spring IOC容器是怎么实现对象的创建和依赖的?

* 根据Bean配置信息在容器内部创建Bean定义注册表 
* 根据注册表加载、实例化bean、建立Bean与Bean之间的依赖关系 
* 将这些准备就绪的Bean放到Map缓存池中，等待应用程序调用

## Spring容器(Bean工厂)可简单分成两种

* `BeanFactory` 是最基础、面向Spring的 
* `ApplicationContext` 是BeanFactory的子类

没有特殊要求的情况下，应该使用ApplicationContext完成。
因为BeanFactory能完成的事情，ApplicationContext都能完成，并且提供了更多接近现在开发的功能。

## 总结

* 在 Spring 开发中，由 IOC 容器控制对象的创建、初始化、销毁等。 
* 这也就实现了对象控制权的反转，由我们对对象的控制转变成了Spring IOC 对对象的控制。 
* DI：是 IOC 的具体实现。
* 程序把依赖交给容器，容器帮你管理依赖。



