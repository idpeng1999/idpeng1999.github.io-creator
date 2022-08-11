---
title: "Flyway使用教程"
date: 2022-04-07T23:55:57+08:00 
draft: false
categories: [工具教程]
---

[官网](https://flywaydb.org/documentation/)

<br>

[引入Maven plugin](https://flywaydb.org/documentation/usage/maven/)

```
   <plugin>
      <groupId>org.flywaydb</groupId>
      <artifactId>flyway-maven-plugin</artifactId>
      <version>6.2.4</version>
      <configuration>
      <user>root</user>
      <password>root</password>
      <url>jdbc:mysql://localhost:3306/xxx</url>
      </configuration>
   </plugin>

```
<br>

[创建目录](https://flywaydb.org/documentation/concepts/migrations#versioned-migrations)

* 在`resources`下创建目录`db`
* 在目录`db`创建目录`migration`
* 在目录`migration`下创建文件`V1__Create_User.sql`
* 在文件`V1__Create_User.sql`下写相应sql

如图

![创建目录图](/img/Flyway使用教程/创建目录图.png)

```
mvn flyway:clean
```

```
mvn flyway:migrate
```




