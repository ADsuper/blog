---
title: 基于Hexo-Github---搭建个人博客笔记
date: 2017-03-19 22:32:26
tags:
---
## 前言:
###### 为了搭建这个博客，踩得坑不计其数，说焦头烂额也不为过．
###### 参考博客：　

[基于Hexo+GitHub Pages 搭建个人博客教程](http://xuhaoblog.com/hexo-github-pages.html)

---
<!--more-->
## 正文： 

### 一、环境的搭建
- **Note.js下载和安装**   
   
    1.下载地址：[https://nodejs.org/en/download/](https://nodejs.org/en/download/)   
    2.windows下安装非常简单     参考地址：[http://www.runoob.com/nodejs/nodejs-install-setup.html](http://www.runoob.com/nodejs/nodejs-install-setup.html)
 
- **Git下载和安装**    
    
    1.下载地址：https://git-scm.com/download/   
    2.windows下安装也很简单，参考地址：http://jingyan.baidu.com/article/90895e0fb3495f64ed6b0b50.html   
### 二、安装Hexo    

1.  桌面上鼠标右键打开Git Bash。
2.  输入安装命令    
```
npm install -g hexo-cli

```
3.  选择硬盘目录作为存放文件的路径    

```
hexo init e:\blog  #在E盘先创建一个blog文件夹存放文件
```

4.  进入该目录后再进行其他操作   

```
cd e:\blog

```

5.  执行安装依赖包的命令     

```
npm install

```

6.  生成部署文件，启动本地服务

```
hexo g   # 或者hexo generate
     
hexo s   # 或者hexo server，可以在http://localhost:4000/ 查看
```
现在我们打开  [http://localhost:4000/ ](http://note.youdao.com/)就可以看到我们刚才搭建的本地博客了，Hexo会默认生成一个Hello World的博文。 停止是ctrl+c

###### hexo几个常用命令    


```

hexo generate (hexo g) 生成静态文件，会在当前目录下生成一个新的叫做public的文件夹
hexo server (hexo s) 启动本地web服务，用于博客的预览
hexo deploy (hexo d) 部署博客到远端服务器
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
```

### 三、github Pages设置     

1. 登录github官网创建github账号： [http://www.github.com/](http://www.github.com/)  
2. 创建仓库:    
    点击右侧+号，new repository  
3. 仓库名字必须是 username/username.github.io ，这是特殊的命名约定。    
    username  就是注册的github账号名字
4. ##### 配置 ssh       
- 检查本地是否存在 ssh ，如果存在就删除 .ssh文件夹      

```
    ls -al ~/.ssh

```

- 设置 name 和 email ，注意：这里的那么和email是随意的，并没有特别的限定   

```
git config --global user.name "<your name>"
git config --global user.email "<your email>"

```
- 生成 ssh 秘钥  ，这里的邮箱是注册  github  的邮箱

```
ssh-keygen -t rsa -C "XXXXX@qq.com"

```
- 一路回车，可以设置密码，如果设置要记住后边要用       

    这一步在~/.ssh/下生成了两个文件id_rsa 和 id_rsa.pub  
     

- 打开 id_rsa.pub 复制全部内容，这就是 ssh 秘钥    
- 配置 ssh 秘钥    
      
    在自己的 github 主页，点击右侧头像下的 setting  ，选择 SSH and GPG keys ,   
         
    然后点击 New SSH key，粘贴刚才复制的 SSH 保存。
- 检查是否配置成功  ，输入以下命令

```
ssh git@github.com

```
- 成功的话会显示以下内容

```

The authenticity of host 'github.com (192.30.252.128)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,192.30.252.128' (RSA) to the list of known hosts.
Hi git-xuhao! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```

### 四、部署到 github    
1. 配置 _config.yml ，在自己创建的 blog 目录下 ，最下方。

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
# ssh://git@github.com/git-xuhao/git-xuhao.github.io
deploy:
  type: git
  repo: ssh://git@github.com/git-xuhao/git-xuhao.github.io
  branch: master
```

###### 其中，repo是我们刚刚建立的远程仓库，换成你自己的仓库，同时因为刚才配置了SSH-Key，所以必须是SSH形式的URL。值得注意的是，每一个: 后面都必须有一个空格，否则会引起错误      

2. 安装  git 包  

```
npm install hexo-deployer-git --save

```

3. 部署到 github 上   

```
hexo deploy

```

4. 现在我们可以通过访问 http://adsuper.github.io/ 来访问我们自己的博客啦，其中链接是自己的仓库名。      

### 五、Hexo 配置文件     
常用到的配置文件一共有两个，分别是blog根目录下的 _config.yml 和 主题下的 _config.yml ，(themes文件夹的为主题)；   
- 关于配置文件的具体描述请参考： [https://hexo.io/zh-cn/docs/configuration.html](https://hexo.io/zh-cn/docs/configuration.html)    

### 六、如何使用？    
1. 新建一篇博文可通过以下的命令 ，要在bolg根目录下打开 Git Bash

```
hexo new "name"
```
         
其中name为博文的名字，建立完成之后，可以在./source/_posts文件夹下发现我们刚刚建立的 name.md文件
2. 博文写好之后，在每次发布之前，我们要先将写好的博客生成静态文件，执行以下命令 

```
hexo g

```

3. 静态文件生成之后，便可以部署到GitHub上  

```
hexo d

```  

            
然后打开我们的博客，就可以看到我们刚刚新建的博文了
### 七、主题推荐   

     
Hexo提供了许多的主题可供我们选择和使用，在./themes目录下存放主题。刚才默认生成的博客用的就是默认的主题landscape。   
- 主题推荐请参考： [https://github.com/hexojs/hexo/wiki/Themes](https://github.com/hexojs/hexo/wiki/Themes)    
    

- 我自己使用的是 Next 主题。   
      

- Next主题的配置方法参考： [http://theme-next.iissnan.com/getting-started.html](http://theme-next.iissnan.com/getting-started.html)  




