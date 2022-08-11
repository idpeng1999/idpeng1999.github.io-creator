---
title: "MyBatis Generator使用教程"
date: 2022-04-08T22:09:30+08:00 
draft: false
categories: [工具教程]
---

**Mybatis Generator（MBG）的作用 ：根据库中的表自动生成dao、mapper映射文件、实体类**

* 在`pom.xml`添加配置
```
<plugins>
      <plugin>
        <groupId>org.mybatis.generator</groupId>
        <artifactId>mybatis-generator-maven-plugin</artifactId>
        <version>1.3.2</version>
        <dependencies>
          <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.48</version>
          </dependency>
        </dependencies>
        <configuration>
          <!--指定generatorConfig.xml 配置文件的路径 -->
          <configurationFile>${basedir}/src/main/resources/generatorConfig.xml</configurationFile>
          <overwrite>true</overwrite>
        </configuration>
      </plugin>
    </plugins>
```

* 将`generatorConfig.xml`配置文件放入`main/resource`目录下

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
  PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
  "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
    <context id="test" targetRuntime="MyBatis3">
        <plugin type="org.mybatis.generator.plugins.EqualsHashCodePlugin"/>
        <plugin type="org.mybatis.generator.plugins.SerializablePlugin"/>
        <plugin type="org.mybatis.generator.plugins.ToStringPlugin"/>
        <commentGenerator>
            <!-- 这个元素用来去除指定生成的注释中是否包含生成的日期 false:表示包含 -->
            <!-- 如果生成日期，会造成即使修改一个字段，整个实体类所有属性都会发生变化，不利于版本控制，所以设置为true -->
            <property name="suppressDate" value="true" />
            <!-- 是否去除自动生成的注释 true：是 ： false:否 -->
            <property name="suppressAllComments" value="true" />
        </commentGenerator>
        <!--数据库链接URL，用户名、密码 -->
        <jdbcConnection driverClass="com.mysql.jdbc.Driver"
            connectionURL="jdbc:mysql://localhost:3306/test" userId="root" password="root">
            </jdbcConnection>
        <javaTypeResolver>
            <!-- 浮点精度更高 -->
            <property name="forceBigDecimals" value="false" />
        </javaTypeResolver>
        <!-- 生成模型(entity)的包名和位置 -->
        <javaModelGenerator targetPackage="com.bz.entity"
            targetProject="src/main/java">
            <property name="enableSubPackages" value="true" />  <!-- enableSubPackages：是否要合并当前两个包    合并之后的包结构是src/main/java/com.bz.entity -->
            <property name="trimStrings" value="true" />        <!-- 是否去除生成实体类中的空格 -->
        </javaModelGenerator>

        <!-- 生成映射文件的包名和位置 -->
        <sqlMapGenerator targetPackage="com.bz.mapper"
            targetProject="src/main/resources">
            <property name="enableSubPackages" value="true" />
        </sqlMapGenerator>

        <!-- 生成DAO的包名和位置 -->
        <javaClientGenerator type="XMLMAPPER"
            targetPackage="com.bz.dao" targetProject="src/main/java">    <!--类型就是XMLMAPPER，不用改-->
            <property name="enableSubPackages" value="true" />
        </javaClientGenerator>
        
        <!-- 数据库中生成哪些表 有多少表就写几个table标签
             tableName：数据库中表名    domainObjectName：生成的实体类名 -->
        <table tableName="files" domainObjectName="Files"></table>

    </context>

</generatorConfiguration>
```

需要修改的有：

* 数据库链接URL，用户名、密码 
* 生成模型(entity)的包名 
* 生成映射文件的包名 
* 生成DAO的包名 
* 数据库中生成哪些表

* 自动在设定位置生成dao、mapper映射文件、实体类

```
mvn mybatis-generator:generate
```


