---
title: "为什么重写equals时必须重写hashCode方法？"
date: 2022-03-10T19:27:38+08:00
draft: false
categories: [java知识]
---

* 因为两个相等的对象的`hashCode`值必须是相等。
* 也就是说如果`equals`方法判断两个对象是相等的，那这两个对象的`hashCode`值也要相等。
* 如果重写`equals()`时没有重写`hashCode()`方法的话就可能会导致`equals`方法判断是相等的两个对象,`hashCode`值却不相等。
