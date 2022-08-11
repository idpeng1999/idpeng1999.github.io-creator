---
title: "SpringBoot中的5种跨域"
date: 2022-04-01T20:30:57+08:00
draft: false
categories: [java知识]
---
## 为什么会出现跨域问题

* 出于浏览器的同源策略限制。
* 同源策略（Sameoriginpolicy）是一种约定，它是浏览器最核心也最基本的安全功能，
如果缺少了同源策略，则浏览器的正常功能可能都会受到影响。 
* 可以说Web是构建在同源策略基础之上的，浏览器只是针对同源策略的一种实现。 
* 同源策略会阻止一个域的javascript脚本和另外一个域的内容进行交互。
所谓同源（即指在同一个域）就是两个页面具有相同的协议（protocol），主机（host）和端口号（port）。

## 什么是跨域

当一个请求url的协议、域名、端口三者之间任意一个与当前页面url不同即为跨域

![跨域](/img/SpringBoot中的5种跨域/1.png)

## 非同源限制

1. 无法读取非同源网页的 Cookie、LocalStorage 和 IndexedDB
2. 无法接触非同源网页的 DOM
3. 无法向非同源地址发送 AJAX 请求

## java后端实现`CORS`跨域请求的方式

对于 CORS的跨域请求，主要有以下几种方式可供选择：

1. 返回新的CorsFilter
2. 重写 WebMvcConfigurer
3. 使用注解 @CrossOrigin
4. 手动设置响应头 (HttpServletResponse)
5. 自定web filter实现跨域(推荐)

### 1.返回新的CorsFilter

在任意配置类，返回一个 新的 CorsFIlter Bean ，并添加映射路径和具体的CORS配置路径。

```java
@Configuration
public class GlobalCorsConfig {
    @Bean
    public CorsFilter corsFilter() {
        //1. 添加 CORS配置信息
        CorsConfiguration config = new CorsConfiguration();
        //放行哪些原始域
        config.addAllowedOrigin("*");
        //是否发送 Cookie
        config.setAllowCredentials(true);
        //放行哪些请求方式
        config.addAllowedMethod("*");
        //放行哪些原始请求头部信息
        config.addAllowedHeader("*");
        //暴露哪些头部信息
        config.addExposedHeader("*");
        //2. 添加映射路径
        UrlBasedCorsConfigurationSource corsConfigurationSource = new UrlBasedCorsConfigurationSource();
        corsConfigurationSource.registerCorsConfiguration("/**",config);
        //3. 返回新的CorsFilter
        return new CorsFilter(corsConfigurationSource);
    }
}
```

### 2.重写 WebMvcConfigurer

```java
@Configuration
public class CorsConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                //是否发送Cookie
                .allowCredentials(true)
                //放行哪些原始域
                .allowedOrigins("*")
                .allowedMethods(new String[]{"GET", "POST", "PUT", "DELETE"})
                .allowedHeaders("*")
                .exposedHeaders("*");
    }
}
```

### 3.使用注解 @CrossOrigin

在控制器(类上)上使用注解 @CrossOrigin，表示该类的所有方法允许跨域。

```java
@RestController
@CrossOrigin(origins = "*")
public class HelloController {
    @RequestMapping("/hello")
    public String hello() {
        return "hello world";
    }
}
```

在方法上使用注解 @CrossOrigin

```java
@RequestMapping("/hello")
    @CrossOrigin(origins = "*")
     //@CrossOrigin(value = "http://localhost:8081") //指定具体ip允许跨域
    public String hello() {
        return "hello world";
    }
```

### 4.手动设置响应头 (HttpServletResponse)

使用 HttpServletResponse 对象添加响应头(Access-Control-Allow-Origin)来授权原始域，
这里 Origin的值也可以设置为 “*”,表示全部放行。

```java
@RequestMapping("/index")
public String index(HttpServletResponse response) {
    response.addHeader("Access-Allow-Control-Origin","*");
    return "index";
}
```

### 5.自定web filter实现跨域(推荐)

首先编写一个过滤器，可以起名字为MyCorsFilter.java

```java
package com.mesnac.aop;

import java.io.IOException;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.http.HttpServletResponse;
import org.springframework.stereotype.Component;

@Component
public class MyCorsFilter implements Filter {
  public void doFilter(ServletRequest req, ServletResponse res, FilterChain chain) throws IOException, ServletException {
    HttpServletResponse response = (HttpServletResponse) res;
    response.setHeader("Access-Control-Allow-Origin", "*");
    response.setHeader("Access-Control-Allow-Methods", "POST, GET, OPTIONS, DELETE");
    response.setHeader("Access-Control-Max-Age", "3600");
    response.setHeader("Access-Control-Allow-Headers", "x-requested-with,content-type");
    chain.doFilter(req, res);
  }
  public void init(FilterConfig filterConfig) {}
  public void destroy() {}
}
```
