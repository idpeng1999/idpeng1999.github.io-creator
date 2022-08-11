---
title: "Docker挂载问题解决"
date: 2021-11-09T23:24:00+08:00
draft: false
categories: [各种问题]
---

[题目地址](https://github.com/hcsp/practise-docker-run)

## docker desktop win10挂载问题解决

系统：win10

* docker pull blindpirate/hcsp-quiz

尝试自己编写一个docker run命令，完成以下要求： 

* 使用交互式命令行模式(-it)启动Docker容器。 
* 向启动的Docker容器内挂载一个文件（卷），使得容器内能够读取到/app/config.txt文件，其内容为字符串"ABC"。 
* 向启动的Docker容器内传递一个环境变量HCSP_ENV=DEF。 
* 为启动的Docker容器设置要执行的命令：java Main。 
* 如果一切正确，命令行会输出： 
* 答案是: XXXXX 
* The answer is: XXXXXXX

**提示未winpty**

```
docker run -e HCSP_ENV=DEF -itv //e/xiedaimala/practise-docker-run/config.txt:/app/config.txt blindpirate/hcsp-quiz
```

![提示未winpty](/img/docker挂载问题解决/img.png)

**未挂载**

```
winpty docker run -e HCSP_ENV=DEF -itv /e/xiedaimala/practise-docker-run/config.txt:/app/config.txt blindpirate/hcsp-quiz
```

![未挂载](/img/docker挂载问题解决/img_2.png)

**成功**

```
winpty docker run -e HCSP_ENV=DEF -itv //e/xiedaimala/practise-docker-run/config.txt:/app/config.txt blindpirate/hcsp-quiz
```

![成功](/img/docker挂载问题解决/img_1.png)
