---
title: "Maven与包"
date: 2021-09-09T22:57:35+08:00
draft: false
categories: [java知识]
---
## jar
jar是将很多类文件打包后的一个压缩包,导入 jar 后,可以直接使用里面的类或调用其中的功能。
## java包的原理
### 传递性依赖
我们依赖的包还依赖了别的类，这种依赖是具有传递性的。
传递性依赖带来的最大的问题就是：
* 我们在 -classpath 后会添加项目依赖的各种各样的 jar 包；
* 如果两个仅仅不同版本的 jar 包被同时写进了 -classpath 参数里面；
* JVM 在 classpath 中寻找类文件的顺序是从前找到后的，也就是说如果有两个仅仅不同版本的 jar ：demo-1.0.jar 和 demo-2.0.jar ，哪个放在前面哪个就会被使用。
* 如果 demo-1.0.jar 的顺序在 demo-2.0.jar 之前，就会使用demo-1.0.jar加载的类文件，这样的话高版本的jar就会不生效。
## maven包的管理
Maven 是一个项目管理工具它包含：
1. 一个项目对象模型
2. 一组标准集合 
3. 一个项目生命周期 
4. 一个依赖管理系统
5. 用来运行定义在生命周期阶段中插件目标的逻辑
### maven怎么进行管理
1. Maven 包管理的做法是：Convention over configuration（约定优于配置原则），体现在 POM。 
2. POM是 Maven 工程的基本工作单元，是一个 XML 文件。 
3. 该文件中包含了项目的基本信息，用于描述项目如何构建，声明项目依赖等等。

#### pom.xml

```java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>hcsp</groupId>
    <artifactId>fix-bug-in-integer-equals</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <profiles>
        <profile>
            <id>aliyunMavenMirror</id>
            <activation>
                <activeByDefault>true</activeByDefault>
            </activation>
            <pluginRepositories>
                <pluginRepository>
                    <id>alimaven</id>
                    <name>aliyun maven</name>
                    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
                </pluginRepository>
            </pluginRepositories>
            <repositories>
                <repository>
                    <id>alimaven</id>
                    <name>aliyun maven</name>
                    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
                </repository>
            </repositories>
        </profile>
        <profile>
            <id>mavenCentral</id>
            <pluginRepositories>
                <pluginRepository>
                    <id>mavenCentral</id>
                    <name>mavenCentral</name>
                    <url>https://repo.maven.apache.org/maven2</url>
                </pluginRepository>
            </pluginRepositories>
            <repositories>
                <repository>
                    <id>mavenCentral</id>
                    <name>mavenCentral</name>
                    <url>https://repo.maven.apache.org/maven2</url>
                </repository>
            </repositories>
        </profile>
    </profiles>
    <dependencies>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.6.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>5.6.0</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>2.22.1</version>
                <configuration>
                    <argLine>-Dfile.encoding=UTF-8</argLine>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```
#### 引入第三方包
```java
<dependencies>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.6.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>5.6.0</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
```

```java
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>5.6.0</version>
    <scope>test</scope>
</dependency>
```
里面加入了junit-jupiter-engine的jar
1. 如果在本地仓库没有找到对应的 jar 包，Maven 就会从远程的中央仓库进行下载，然后放到本地仓库中。 
2. Maven [中央仓库位置](https://repo1.maven.org/maven2/)
## 包冲突及解决办法
### 包冲突
![包冲突示意图](/img/maven与包/包冲突示意图.png)<br>
相比于C1来说，C2这个第三方包离项目更接近，因此Maven会自动帮你把C1去除，而保留C2。
### 解决冲突的办法
1. 直接依赖C2
2. 排除C1
3. 通过Maven helper插件来解决包冲突问题
```java
排除
<dependency>
  <groupId>xxx</groupId>
  <artifactId>xxx</artifactId>
  <version>1.0.0</version>
  <exclusions>
    <exclusion>
        <groupId>yyy</groupId>
      <artifactId>yyy</artifactId>
    </exclusion>
  </exclusions>
</dependency>
```
排除了xxx依赖中的后代yyy依赖，也可以解决包冲突的问题


