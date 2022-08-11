---
title: "Maven构建"
date: 2021-11-21T22:25:41+08:00
draft: false
categories: [java知识]
---

## 生命周期(lifecycle)

* default生命周期处理项目部署
* clean生命周期处理项目清理
* site生命周期处理项目站点文档的创建

## 阶段(phase)

![阶段](/img/Maven构建/2.png)

每个构建生命周期都由不同的构建阶段列表定义，其中构建阶段表示生命周期中的一个阶段。
例如，`default`生命周期包括以下阶段：

* validate - 验证项目是否正确，并提供所有必要的信息 
* compile - 编译项目源代码 
* test - 使用合适的单元测试框架测试编译后的源代码。这些测试不需要打包或部署代码 
* package - 将编译后的代码以其可分发的格式打包，例如JAR 
* verify - 对集成测试的结果进行检查，以确保满足质量标准 
* install -将包安装到本地存储库中，作为本地其他项目中的依赖项使用 
* deploy - 在集成或发布环境中操作，将最终包复制到远程存储库，以便与其他开发人员和项目共享

这些生命周期阶段(加上这里没有显示的其他生命周期阶段)按顺序执行，以完成`default`生命周期。
鉴于上面的生命周期阶段，这意味着当使用default生命周期时。
Maven将首先验证项目，然后将视图编译源代码，
运行测试，打包二进制文件(如jar)，
运行集成测试方案，验证集成测试，
安装验证过的包到本地存储库，然后将安装包部署到远程存储库。

## 插件(plugin)的目标(goal)

Maven的操作是基于不同的插件的不同目标来实现的

**例**

`mvn clean`
使用的参数是clean阶段，而实际执行的是maven-clean-plugin插件的clean目标。

**常用的插件**

[插件](http://maven.apache.org/plugins/index.html)

1. maven-clean-plugin
2. maven-resouces-plugin
3. maven-compiler-plugin
4. maven-deploy-plugin
5. maven-surefire-plugin
6. maven-install-plugin

**直接运行插件**

可使用`插件名:目标名`的参数形式直接运行某插件的某目标。

例如：

`mvn dependency:copy-dependencies`
以上命令执行了dependency插件的copy-dependencies目标。

**阶段(phase)和插件目标(goal)可以同时使用**

例如：

`mvn clean dependency:copy-dependencies package`
执行了clean周期的pre-clean和clean阶段，
dependency插件的copy-dependencies目标，
default周期package阶段及package之前的所有阶段。

## 绑定的整个工作原理

[官方文档](http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#Lifecycle_Reference)

![Maven坐标](/img/Maven构建/3.png)

* groupId：组织标识名（简单理解成 包名）
* artifactId：项目名称
* version：项目的当前版本
* packaging：项目的打包方式，最为常见的jar和war两种（项目中继承的话，为pom）
* classifier: 该元素用来帮助定义构建输出的一些附属构件（不能被直接定义）

依赖性管理，在`pom.xml`文件中`<dependency></dependency>`中

### 依赖传递

若A依赖B，B依赖C，则A也依赖于C（A对于C为间接依赖）

### 仓库管理

仓库用来统一存储所有Maven共享构建的位置，

根据maven坐标，目录方式：`groupId/artifactId/version/artifactId-version.packaging`
就可以唯一确定一个构建。

每个用户只有一个本地仓库，默认是在`${user.home}/.m2/repository/`，`${user.home}`代表的是用户目录

1. Maven默认的远程仓库：URL：[http://search.maven.org/](http://search.maven.org/)，我们需要引用外部的包时，可以从上面查到相关的GroupId、版本号等信息
2. 私服：是一种特殊的远程仓库，架设在局域网内的仓库（一般公司内部都会有一个自己的私服）

<br>
<br>

![Maven](/img/Maven构建/1.png)
