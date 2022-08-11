---
title: "Drop、delete区别？"
date: 2022-03-10T20:37:52+08:00
draft: false
categories: [MySQL知识]
---

### 用法不同

* `drop`(丢弃数据):`drop table`表名 ，直接将表都删除掉，在删除表的时候使用。 
* `delete`（删除数据）:`delete from 表名 where 列名=值`，删除某一列的数据

---

* 不带`where`子句的`delete`、以及`drop`都会删除表内的数据
* 但是`delete`只删除数据不删除表的结构(定义)
* 执行`drop`语句，此表的结构也会删除，也就是执行`drop`之后对应的表不复存在。
