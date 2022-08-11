---
title: "Git快捷配置"
date: 2022-05-12T13:34:41+08:00
draft: false
categories: [笔记]
---
## 查看git快捷配置

```shell
cat ~/.bashrc
```

## 修改git快捷配置

```shell
vi ~/.bashrc
```

例子

```text
alias ga="git add"
alias gm="git commit -m"
alias gc="git commit -v"
alias gl="git pull"
alias gp="git push"
alias gco="git checkout"
alias gst="git status -sb"
alias glog="git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit -- | less"
```
