---
title: "Git本地仓库与远程仓库"
date: 2021-09-09T21:59:31+08:00
draft: false
categories: [工具教程]
---
# git系列操作
## git六行配置
```
git config --global user.name 你的英文名
git config --global user.email 你的邮箱
git config --global push.default simple
git config --global core.quotepath false
git config --global core.editor "code --wait"
git config --global core.autocrlf input
```
注意：
* 上面的英文名和邮箱跟 GitHub 没有关系。
* 可以跟 GitHub 的用户名和邮箱保持一致，也可以不一致。

## 新建代码库
```
# 在当前目录新建一个 Git 代码库
git init

# 新建一个目录，将其初始化为 Git 代码库
git init [project-name]

# 下载一个项目和它的整个代码历史
git clone [url]
```
## 配置文件
```
# 显示当前的 Git 配置
git config --list

# 编辑 Git 配置文件
git config -e [--global]

```
## 增加/删除文件
```
# 添加指定文件到暂存区
git add [file1] [file2] ...

# 添加指定目录到暂存区，包括子目录
git add [dir]

# 添加当前目录的所有文件到暂存区
git add .

# 删除工作区文件，并且将这次删除放入暂存区
git rm [file1] [file2] ...

# 停止追踪指定文件，但该文件会保留在工作区
git rm --cached [file]

# 改名文件，并且将这个改名放入暂存区
git mv [file-original] [file-renamed]


代码提交
# 提交暂存区到仓库区
git commit -m [message]

# 提交暂存区的指定文件到仓库区
git commit [file1] [file2] ... -m [message]

# 提交工作区自上次 commit 之后的变化，直接到仓库区
git commit -a

# 提交时显示所有 diff 信息(推荐)
git commit -v

# 使用一次新的 commit，替代上一次提交
# 如果代码没有任何新变化，则用来改写上一次 commit 的提交信息
git commit --amend -m [message]

# 重做上一次 commit，并包括指定文件的新变化
git commit --amend   ...
```
## 分支
```
# 列出所有本地分支
git branch

# 列出所有远程分支
git branch -r

# 列出所有本地分支和远程分支
git branch -a

# 新建一个分支，但依然停留在当前分支
git branch [branch-name]

# 新建一个分支，并切换到该分支
git checkout -b [branch]

# 新建一个分支，指向指定 commit
git branch [branch] [commit]

# 新建一个分支，与指定的远程分支建立追踪关系
git branch --track [branch] [remote-branch]

# 切换到指定分支，并更新工作区
git checkout [branch-name]

# 建立追踪关系，在现有分支与指定的远程分支之间
git branch --set-upstream [branch] [remote-branch]

# 合并指定分支到当前分支
git merge [branch]

# 选择一个 commit，合并进当前分支
git cherry-pick [commit]

# 删除分支
git branch -d [branch-name]

# 删除远程分支
git push origin --delete 
git branch -dr
```
## 提交代码
```
git pull 提交代码到远程仓库
git push -u origin master 提交本地指定分支master代码到远程仓库
```

