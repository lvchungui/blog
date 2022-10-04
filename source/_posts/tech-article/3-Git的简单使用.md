---
title: Git的简单使用
categories: 
- 技术

tags:
- Git
---


- 这里介绍两种简单方法，一种是使用命令的方式，另一种是图形化的方式，这里推荐使用图形化方式上传。先下载安装 git 和 tortoise git，必须先安装 git 才能安装 tortoise git
- git 下载地址：https://git-scm.com/
- git 安装教程：https://blog.csdn.net/qq_46351233/article/details/124733661
- tortoise git 下载地址：https://tortoisegit.org/download/
- tortoise git 安装教程：http://t.zoukankan.com/jpfss-p-8027543.html

## 以git命令方式上传

1. 复制仓库地址→右键选择`Git Bash Here`→在命令框中输入`git clone 仓库地址`即可把仓库克隆到本地
2. 把自己的代码放到刚克隆过来的文件夹里→右键选择`Git Bash Here`→输入`git add .`回车→输入`git commit -m"提交日志"`回车→最后输入`git pull`回车即可上传成功

## 以图形化方式上传

1. git add 
   - 右击标记为 蓝色 ? (表示该文件未使用 git 管理) 的目录，弹出的对话框中勾选具体需要管理的文件，勾选完毕点击 ok 即可，此时图标变成红色感叹号(表示该文件被git管理，但是未提交内容)

        ![](../images/12.png)

3. git commit
   + 将修改内容提交到本地每提交一次，就是一个版本. 比如开发完某个功能模块，就可以提交一次了，后续进行版本回退都是以提交为准.注意: 此时只是提交到本地，Github 上还看不到代码变更，右键选择红色感叹号目录，选择 Git commit -> master
   + 此时弹出了一个对话框. 可以在此处看到都需要提交哪些文件, 以及每个文件的具体改动情况. 并且需要输入提交日志. 描述这次提交的具体改动原因是什么. 这个日志是后续进行版本回退的重要参考依据

        ![](../images/13.png)

        ![](../images/14.png)

4. git push
   + 提交的内容需要同步到服务器上, 才能让其他人看到改动. 使用 push 即可，右键需要 push 的目录, 点击 push


- 解决no supported authentication methods avaiable
   + 找到TortoiseGit ->Settings（设置）->Network（网络）
   + 将SSH client指向E:\git\Git\usr\bin\ssh.exe （我的Git工具安装E盘）,这里更改ssh 路径的时候，要把上面的勾打上，点击应用，再确定

        ![](../images/15.png)