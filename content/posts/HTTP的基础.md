---
title: "HTTP的基础"
date: 2021-09-13T15:33:51+08:00
draft: false
categories: [HTML]
---
## Http方法与状态码

[http方法](https://www.runoob.com/http/http-methods.html)


* GET 拿   
* POST 发送  

```
GET / HTTP/1.1     //GET请求根路径 使用HTTP1.1协议
Host: xiedaimala.com
User-Agent:  //用户代理（浏览器） 可根据查看相关信息
```
[Http状态码](https://www.runoob.com/http/http-status-codes.html)
`200`请求成功。一般用于GET与POST请求<br>

[http猫](https://http.cat/)

## HTTP的header与body
重要的header 
* Accept
* Cookie
* User-Agent  //浏览器标识
* Referer   //上一个页面是什么
```
Referer: http://idpeng.xyz/
```
* Content-type //下载或者图片
```
content-type: text/html; charset=utf-8
```
* Set-Cookie  //登录后服务器自动设置的cookie

http是无状态的