---
title: "Object有哪些方法？"
date: 2022-03-10T16:33:22+08:00
draft: false
categories: [java知识]
---
* Object类，属于java.lang包，位于类层次结构树的顶部。

* 每个类都是Object类的直接或间接的后代。

* 使用或编写的每个类都继承Object的实例方法。


常用方法：

* `getClass 方法` final 方法、获取对象的运行时 class 对象，class 对象就是描述对象所属类的对象。
* `hashCode 方法` 该方法主要用于获取对象的散列值。Object 中该方法默认返回的是对象的堆内存地址。
* `equals 方法` 该方法用于比较两个对象，如果这两个对象引用指向的是同一个对象，那么返回 true，否则返回 false。
* `clone 方法` 该方法是保护方法，实现对象的浅复制，只有实现了 Cloneable 接口才可以调用该方法，否则抛出 CloneNotSupportedException 异常。
* `toString 方法` 返回一个 String 对象，一般子类都有覆盖。默认返回格式如下：对象的 class 名称 + @ + hashCode 的十六进制字符串。
* `wait 方法` 当timeout 为 0，即不等待。
