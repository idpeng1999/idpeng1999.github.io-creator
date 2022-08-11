---
title: "Apidoc使用教程"
date: 2022-05-14T17:16:58+08:00
draft: false
categories: [工具教程]
---

[官方教程](https://apidocjs.com/)

## 配置

1. 安装node.js
2. 安装apidoc
```text
npm install apidoc -g
```

3. 在项目根目录下新建apidoc.json文件
![apidoc.json](/img/Apidoc使用教程/img.png)
```text
{
  "name": "wxshop",
  "version": "1.0.0",
  "description": "小微店铺",
  "title": "小微店铺",
  "url" : "https://localhost:8080/api/v1"
}
```

## 使用样例
```java
/**
     * @api {post} /code 请求验证码
     * @apiName GetCode
     * @apiGroup 登录与鉴权
     *
     * @apiHeader {String} Accept application/json
     * @apiHeader {String} Content-Type application/json
     *
     * @apiParam {String} tel 手机号码
     * @apiParamExample {json} Request-Example:
     *          {
     *              "tel": "13012345678",
     *          }
     *
     * @apiSuccessExample Success-Response:
     *     HTTP/1.1 200 OK
     * @apiError 400 Bad Request 若用户的请求包含错误
     *
     * @apiErrorExample Error-Response:
     *     HTTP/1.1 400 Bad Request
     *     {
     *       "message": "Bad Request"
     *     }
     */
    /**
     * @param telAndCode 手机号和收到的验证码
     * @param response HTTP response
     */
    @PostMapping("/code")
    public void code(@RequestBody TelAndCode telAndCode,
                     HttpServletResponse response) {
        if (telVerificationService.verifyTelParameter(telAndCode)) {
            authService.sendVerificationCode(telAndCode.getTel());
        } else {
            response.setStatus(HttpStatus.BAD_REQUEST.value());
        }
    }
```

### @api
```text
@api {method} path [title]
```
HTTP接口调用方法、路径及名称

### @apiVersion
```text
@apiVersion version
```
api 版本号

### @apiName
```text
@apiName name
```
api 名称

### @apiGroup
```text
@apiGroup name
```
api 分组

### @apiHeader
```text
@apiHeader [(group)] [{type}] [field=defaultValue] [description]
```
请求头参数

### @apiParam
```text
@apiParam [(group)] [{type}] [field=defaultValue] [description]
```
请求参数

### @apiSuccess
```text
@apiSuccess [(group)] [{type}] field [description]
```
返回数据描述

### @apiSuccessExample
```text
@apiSuccessExample [{type}] [title]
                   example
```
接口成功返回样例

### @apiError
```text
@apiError [(group)] [{type}] field [description]
```
接口失败描述

### @apiErrorExample
```text
@apiErrorExample [{type}] [title]
                 example
```
接口失败返回样例

### @apiDefine
```text
@apiDefine name [title]
                     [description]
```
类似于宏定义，可以被引用

### @apiUse
```text
@apiUse name
```
使用@apiDefine定义的描述

## 生成文档

cd到apidoc.json所在路径（即项目根目录）执行如下命令即可
```text
apidoc -i src/ -o apidoc/
```

* 执行成功后会生成apidoc文件夹;
* 点开apidoc文件夹中`index.html`会发现已经生成的漂亮的api文档。
