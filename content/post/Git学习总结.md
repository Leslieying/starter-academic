---
title: Git学习总结
date: 2018-11-25 20:54:42
summary: " "
draft: false 
---
## Git简介

Git由Linus开发以实现版本控制，（几乎）是现在最流行的版本控制系统。与分布式对应的是集中式管理（Centralized Version Control System），他们的区别是，集中式只有一个总服务器，N个客户端共用一套数据；而分布式是每个客户端都有一整套的镜像数据。Git官网给出了关于Git的详细[文档](https://git-scm.com/doc)（它支持多国语言），所以本文主要是做一个简单的介绍以及对我自己的复习。
另外，Git is free!

## 安装Git

要想学Git，第一步自然从安装开始。不过不同于一些依赖环境的软件，Git安装很简单，去官网找一下就行了。Linux系统（如Ubuntu）直接用`sudo apt-get install git`安装，Windows则下载对应的setup狂按下一步就OK了。

## 使用Git

### 基本命令

相信用Git的人都不会是小白，所以命令行是必须的。下面是一些基本的命令。

```git
1. git config --global user.name/email => 配置你的信息
2. git init => 初始化一个仓库（repository）
3. git add => 添加到缓冲区
4. git commit (-m "message") => 提交 //分add+commit两步走的原因是commit可以提交多个文件
5. git status => 查看状态
6. git log => 查看log日志
7. git rm => 删除文件
```

### 版本回溯

版本管理，形象的就是一条时间线上的不同版本，本质上就是不同的文件。所以要想随意地穿梭于各个版本之间，就必须对每个版本产生一个独一无二的ID。在Git中，commit ID是一串十六进制数字，之所有这么做是避免每个client的ID的重复。此外，在git中有一个指向__当前__版本的HEAD指针，版本的切换其实就是用HEAD指向不同的版本。
说了这么多，其实版本的“倒带”命令很简单，`git reset --hard ID`即可，ID也可以用HEAD^来表示相对版本，每一个^就代表往回走一步。当^太多了怎么办？用HEAD~n来表示回溯n个版本。

### 版本前进

问题来了，回去了怎么回来？用git log找到commit ID，然后reset回来即可。

### 远程仓库

现在我们觉得在本地修修改改没有意思，现在还想把本地文件放在远程仓库托管。  
那么第一个最基本的操作就是把本地和远程关联起来。输入命令`git remote add origin your_url`，这里origin就是远程仓库的名字，是git的默认叫法。而远程仓库可以用GitHub、gitlab、码云等网站注册。  
第二步呢，就是把本地的文件传到远程仓库。命令是`git push -u origin master`，不过呢在这里还要进行验证，Git服务器通过SSH KEY来进行认证，没有SSH KEY怎么办？很简单，生成一个。在命令行里输入`ssh-keygen -t rsa -C "your_email@example.com`即可，生成的密钥在.ssh目录中，分别id_rsa和id_rsa.pub两个文件，.pub的就是公钥，可以用来添加到GitHub中完成连接。  
不过，即便是SSH关联了，在后面git push时也可能要你输入用户名和密码，这是因为你在clone时可能用的是https方式，这时候就要在项目文件夹里的.git/config里修改remote origin url为ssh://git@github.com/name/repos.git即可了。

## 分支管理

分支就是相当于一个平行空间，每一个分支的变化都不会影响其他的分支。在Git中，主分支称为master，用户可以通过创建额外的分支来进行开发，然后和主分支进行合并，完成修改，之后，再将分支删除掉。以下是常用命令:

``` git
0. git branch => 查看分支 //当加上<branch.name>时就是创建分支
1. git checkout => 切换分支
2. git merge => 合并分支
3. git branch -d => 删除分支
4. git pull => 更新本地仓库
```

在合并中，很可能会出现矛盾，这会让git不知道听哪一个的。所以就要手动解决冲突，然后再进行合并。

## 分支的本质

要用好Git，就要理解好Git分支的原理。Git把我们的工作分成了几个区域:

```shell
0. 工作区(file)
1. 暂存区(stage/index)
2. 版本库(branch)
3. 远程仓库(remote)
```

每一次步骤分别使用add命令将文件添加到暂存区，用commit命令提交到分支中。每次commit之后，就会产生一个提交对象(commit object), 它包含着提交文件的基本信息还有指向tree对象的指针，tree对象记录着文件的结构还有blob对象(就是文件快照)的索引。所以每次提交会产生以下的对象:
`commit object > tree object > blobs`,
每一次提交像一个神经元一样，连成一整个timeline:
`--O--O--O---O`
而分支，其实就是指向这些神经元的指针，而HEAD就是指向当前状态(分支)的指针（如下）。  

{{< figure library="true" src="git_branch.png" title="git_branch" lightbox="true" >}}

所以，当你创建一个新的分支的时候，其实只是换了一个指针，其他的文件都没有变化（有点像C语言是吧）。这使得Git的速度非常快，也是Git超出其他版本控制软件的重要原因或理念。另外一提，Git也是不依赖于网络的，它基于本地资源，可以大大减少对网络的依赖并且提升自身的速度。

## 标签管理

每个版本都会有对应的版本号，其实就是和commit ID一样的东西。但是我们当然不能用那一串十六进制的数值来表示，所以Git支持用户自己给版本打标签，命令同样很简洁明了，如`git tag v1.2`即可，标签是默认在最近的提交上的。

## 参考资料

1. [廖雪峰](https://www.liaoxuefeng.com/wiki/896043488029600)
2. [Git官网](https://git-scm.com/doc)
3. [Git简明教程](http://rogerdudler.github.io/git-guide/index.zh.html)
