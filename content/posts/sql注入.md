---
title: "Sql注入"
date: 2022-03-14T15:25:04+08:00
draft: false
categories: [MySQL知识]
---
## 万能密码

原验证登陆语句:

```mysql
SELECT * FROM admin WHERE Username= '".$username."' AND Password= '".md5($password)."'
```

输入 1′ or 1=1 or ‘1’=’1万能密码语句变为:

```mysql
SELECT * FROM admin WHERE Username='1' OR 1=1 OR '1'='1' AND Password='EDFKGMZDFSDFDSFRRQWERRFGGG'
```

即得到优先级关系：or<and<not，同一优先级默认从左往右计算。

1. 上面’1’=’1’ AND Password=’EDFKGMZDFSDFDSFRRQWERRFGGG’先计算肯定返回false,因为密码是我们乱输入的。(此处是假)
2. Username=’1’ 返回假,没有用户名是1(此处是假)
3. 1=1返回真(此处是真)

以上的结果是: 假 or 真 or 假 返回真。验证通过。