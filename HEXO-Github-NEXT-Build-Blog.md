---
title: HEXO + Github + NEXT Build Blog
date: 2017-12-24 21:42:46
categories: web
tags: Hexo
---

想弄个博客用来记载一些学习笔记，不想租服务器 买域名，HEXO + Github 快速搭建博客最合适。 实际就是在本地机上用markdown editor （比如sublime text) 写好博客, 然后用HEXO 通过SSH 或者 HTTPS的方式发布到Github, 这样就可以网上浏览了。步骤简单。

**1.下载安装 Node.js 和 Gi, 这个google一下下载安装最新版就好了.**
**2. 安装HEXO**
打开git cmd 或者 git shell，cd到你要放博客文件的本地机路径下面 比如c:\blog，然后输入

       $ npm install hexo-cli -g       #安装hexo        
       $ hexo init username.github.io  #在本地机上新建用来放博客的文件夹并初始化
       $ cd username.github.io         #这步忽略的话可能会出现dependency error 
       $ npm install                   #在新建的博客文件夹里安装npm(node的模块管理器)

然后新建的博客文件夹里就会有source, themes之类的子文件夹，都是用来存放跟博客相关的一些文件。比如你的每篇博客会存放在source/_post里，博客的主题会存在themes文件夹里等等。

**3. 写博客**

     $ hexo n "new blog title"          #在本地机新建一篇博客
     $ go to source/_post, edit xxx.md  #在本地机编辑这篇博客
     $ hexo g (generate blog)           #完成创建
     $ hexo s                           #本地机预览 （地址localhost:4000）

**4. 把本地机博客发布（配置）到github**
你得现在github网站上建个账号（已经有的就不必要了），账号里建个公共仓库 （public repository),这仓库得叫username(你github上的用户名）.github.io， 这仓库就是用来放你本地机传上来的博客。在本地博客路径下找到_config文件，找到Deployment，设置如下。意思是用git的方式传送或者发布博客到github

    deploy:
      type: git
      repo: git@github.com:username/username.github.io.git
      branch: master

git的方式有时候会有连接不上的问题，ssh可以参考github上[如何重建ssh key以及加到ssh agent 和github账号上](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)。 注意如果安装了github desktop要确保这个里面的账号和ssh key跟github账号上的一致 （可以在新建ssh key之前删除所有在.ssh文件夹里的文件）。 另外可以试试https的方式，在_config里，把repo: git@github.com:username/username.github.io.git 改成 repo: https://github.com/username/username.github.io

设置好之后， 在本地博客路径下，输入

      $ npm install hexo-deployer-git --save     #先安装一个扩展
      $ hexo d -g                                #完成博客的创建并发布到github

**5. 换主题 **
博客的样子可以换，比如换成next，设置可以参考[NEXT网站](http://theme-next.iissnan.com/getting-started.html)

[参考网站](http://www.wuxubj.cn/2016/08/Hexo-nexT-build-personal-blog/)

