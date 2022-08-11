---
title: "StringBuffer、StringBuilder区别"
date: 2022-03-10T16:32:52+08:00
draft: false
tags: [java]
categories: [java知识]
---
### 区别

* StringBuffer稍慢，但线程安全
* StringBuilder更快，但线程不安全，常用

### 线程安全性

* 如果没有额外声明，所有类的默认都是线程不安全的
