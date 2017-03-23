---
title: Git命令总结
date: 2017-03-21 15:25:01
tags: Git
categories: Git
---

### 前言：     

**由于在搞博客的原因，顺带着多了解了点  Git 命令，欢迎大家指正！**      


---
<!--more-->

### 一、Git工具      

下载地址：[https://git-scm.com/download/](https://git-scm.com/download/)   
安装也很简单，基本就是一直下一步，选默认的就好！   

### 二、常用命令介绍     

##### 1. 本地文件夹与 github 远程仓库建立连接    

在需要建立连接的文件夹，右键 Git Bash 输入：

```
git init
git remote add origin <server>
```
其中，server是 github 远程仓库地址，origin只是仓库的一个别名，这里可以随意变！

##### 2. 将本地的文件，同步到 github 远程仓库上   


```
git add .  #添加所有目录，后边有个点
git commit -m "message" #添加提交说明信息
git push -u origin master   #云端同步
```
##### 3. 把 github 上的文件取回本地   

在本地先建立一个文件夹，右键 Git Bash 输入：

```
git init
git remote add origin <server> # server是远程仓库地址
git fetch –all
git merge origin/master  #这个origin与步骤 1 的那个一致
```

##### 4. 如果两个PC端操作一个远程仓库地址


```

	每次先  git pull 进行同步更新，然后执行步骤 2 
```

##### 5.修改 github 远程仓库地址    

- 第一种方式：在需要修改远程地址的文件夹下  右键 Git Bash 输入：   


```
git remote rm origin	#先删除
git remote add origin <server> #重新添加地址
```
- 第二种方式：找到.git文件夹下的config文件  

    找到 [remote "origin"]，下边的url就是远程仓库地址，修改成自己需要的就好！


