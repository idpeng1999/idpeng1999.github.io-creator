---
title: "Continue、break和return的区别是什么？"
date: 2022-03-10T17:14:47+08:00
draft: false
categories: [java知识]
---
在循环结构中，当循环条件不满足或者循环次数达到要求时，循环会正常结束。
但是，有时候可能需要在循环的过程中，当发生了某种条件之后 ，提前终止循环，
这就需要用到下面几个关键词：

* `continue`：指跳出当前的这一次循环，继续下一次循环。
* `break`：指跳出整个循环体，继续执行循环下面的语句。

`return`：用于跳出所在方法，结束该方法的运行。return 一般有两种用法：

* `return;` ：直接使用 return 结束方法执行，用于没有返回值函数的方法
* `return value;` ：return 一个特定值，用于有返回值函数的方法

下列语句的运行结果是什么？

```java
 public static void main(String[] args) {
        boolean flag = false;
        for (int i = 0; i <= 3; i++) {
            if (i == 0) {
                System.out.println("0");
            } else if (i == 1) {
                System.out.println("1");
                continue;
            } else if (i == 2) {
                System.out.println("2");
                flag = true;
            } else if (i == 3) {
                System.out.println("3");
                break;
            } else if (i == 4) {
                System.out.println("4");
            }
            System.out.println("xixi");
        }
        if (flag) {
            System.out.println("haha");
            return;
        }
        System.out.println("heihei");
    }
```
运行结果:

```
0
xixi
1
2
xixi
3
haha
```
