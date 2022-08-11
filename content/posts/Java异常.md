---
title: "Java异常"
date: 2022-03-10T16:58:49+08:00
draft: false
categories: [java知识]
---
## 异常基本类型

* 异常类的基本类型是`Throwable`类
* 两大子类分别是`Error`和`Exception`

### Error

* 系统错误由Java虚拟机抛出，用`Error`类表示。`Error`类描述的是内部系统错误
* 例如：Java虚拟机崩溃。在程序中不会对`Error`异常进行捕捉和抛出。

### Exception

异常`Exception`又分为`RuntimeException`(运行时异常)和`CheckedException`(检查时异常)

#### RuntimeException(运行时异常)

* 程序运行过程中才可能发生的异常,一般为代码的逻辑错误
* 例如：类型错误转换，空指针异常、找不到指定类等

#### CheckedException(检查时异常)

* 编译期间可以检查到的异常，必须显式的进行处理（捕获或者抛出到上一层）
* 例如：`IOException`, `FileNotFoundException`,`SQLException`等

## 异常处理

### throws（声明异常）

* 在方法头中显式声明该异常，以便于告知方法调用者此方法有异常
* 若父类的方法没有声明异常，则子类继承方法后，也不能声明异常

### try-catch（捕获异常）

* 若执行`try`块的过程中没有发生异常，则跳过`catch`子句
* 若是出现异常，`try`块中剩余语句不再执行。
* 再判断`catch`块的异常类是否是捕获的异常类型，匹配后执行相应的`catch`块中的代码。
* 如果有`finally`的话进入到`finally`里面继续执行。
* `try ctach fianally`中有`return`时，会先执行`return`,但是不会返回。在执行完`finally`后进行返回
* `catch`语句可以有一个或多个，`finally`语句最多一个

## throw,throws关键字区别

* `throw`关键字是用于方法体内部，用来抛出一个Throwable类型的异常
* `throws`关键字用于方法体外部的方法声明部分，用来声明方法可能会抛出某些异常

```java
public static void test()throws Exception{
    throw new Exception("方法test中的Exception");
}  
```

## 常见的几种异常

RuntimeExceptionjava.lang.ArithmeticException(算术异常)
<br>

* java.lang.`NullPointerException`(空指针异常)
* java.lang.`ClassCastException`(类型转换异常)
* java.lang.`IllegalArgumentException`(不合法的参数异常)
* java.lang.`IndexOutOfBoundsException`(数组下标越界异常)

<br>

java.io.IOException(IO流异常)
<br>

* java.lang.`ClassNotFoundException`(没找到指定类异常)
* java.lang.`NoSuchFieldException`(没找到指定字段异常)
* java.lang.`NoSuchMetodException`(没找到指定方法异常)
* java.lang.`IllegalAccessException`(非法访问异常)
* java.lang.`InterruptedException`(中断异常)

