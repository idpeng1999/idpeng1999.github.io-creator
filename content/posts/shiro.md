---
title: "Shiro"
date: 2022-03-16T22:48:35+08:00
draft: false
categories: [java知识]
---
## Shiro框架

是一个轻量级的安全框架，主要提供了 授权、认证、加密、会话管理这几个功能。

## shiro安全数据源有哪些

1. 数据库
2. 静态ini文件
3. session

## Shiro运行流程

比如一个登陆流程：

1. 首先调用Subject.login(token)进行登录，他会委托给SecurityManager 
2. SecurityManager负责真正的身份验证逻辑；它会委托给Authenticator进行身份验证； 
3. Authenticator会把相应的token传入Realm，从Realm获取身份验证信息，
如果没有就返回认证失败，有的话就继续执行操作。

## Shiro 的优点

1. 简单的身份认证, 支持多种数据源；非常简单的加密 API； 
2. 对角色的简单的授权, 支持细粒度的授权(方法级)； 
3. 支持一级缓存，以提升应用程序的性能； 
4. 内置的基于 POJO 企业会话管理, 适用于 Web 以及非 Web 的环境； 
5. 不跟任何的框架或者容器捆绑, 可以独立运行。

## Shiro 的3个核心组件

### Subject

正与系统进行交互的人, 或某一个第三方服务。
所有 Subject 实例都被绑定到一个SecurityManager 上。

### SecurityManager

* Shiro 架构的心脏, 用来协调内部各安全组件, 管理内部组件实例, 并通过它来提供安全管理的各种服务。 
* 当 Shiro 与一个 Subject 进行交互时, 实质上是幕后的 SecurityManager 处理所有繁重的 Subject 安全操作。

### Realms

* 本质上是一个特定安全的 DAO. 当配置 Shiro 时, 必须指定至少一个 Realm 用来进行身份验证和授权。 
* Shiro 提供了多种可用的 Realms 来获取安全相关的数据. 例如关系数据库(JDBC), INI 及属性文件等。 
* 可以定义自己 Realm 实现来代表自定义的数据源。

## 如何配置在 Spring 中配置使用 Shiro


1. 在 web.xml 中配置 Shiro 的 Filter； 
2. 在 Spring 的配置文件中配置 Shiro； 
3. 配置自定义 Realm：实现自定义认证和授权； 
4. 配置 Shiro 实体类使用的缓存策略； 
5. 配置 SecurityManager； 
6. 配置保证 Shiro 内部 Bean 声明周期都得到执行的 Lifecycle Bean 后置处理器； 
7. 配置AOP 式方法级权限检查； 
8. 配置 Shiro Filter