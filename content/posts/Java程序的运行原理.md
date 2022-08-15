---
title: "Java程序的运行原理"
date: 2022-03-10T16:26:18+08:00
draft: false
categories: [JVM]
---
.java --- 编译(compler) --- 字节码(.class) --- JVM

* .class 打包成 .jar
* JVM解析字节码

1. 使用文字编辑软件或集成开发环境编辑 Java 源文件，扩展名为 .java
2. 通过编译 .java 文件，生成同名的 .class 字节码文件
3. 通过 JVM 解释方式，将 .class 字节码文件转变为由 0 或 1 组成的二进制指令（机器码）运行