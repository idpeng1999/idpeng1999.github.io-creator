---
title: "Tomcat端口被占用找不到进程"
date: 2023-01-31T09:43:00+08:00
draft: false
categories: [各种问题]
---

## CMD终止

* 找出占用1099端口的进程,进入windows命令，查看什么进程占用了1099端口 
* 使用命令:`netstat -aon|findstr 1099` 找出占用1099端口的进程
* 然后关闭占用该端口的进程:`taskkill -f -pid 3756`,(3756为进程ID)

## 重置

* 使用`netstat -aon|findstr 1099` 这个命令(find不到端口号)
* 使用命令`netsh winsock reset`
* 重启电脑


