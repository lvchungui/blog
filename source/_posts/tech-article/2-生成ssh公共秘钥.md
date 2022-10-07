---
title: 生成ssh公共秘钥
categories: 
- 技术

tags:
- ssh公共秘钥
---

## 1 设置用户名和邮箱
- 右键选择`Git Bash Here`，在命令框中输入执行下面两条命令

    ~~~
    git config --global user.name “yourname”
    git config --global user.email“your@email.com"
    ~~~

    > 注：yourname是你要设置的名字，your@email是你要设置的邮箱

## 2 删除.ssh文件夹下的 known_hosts

- known_host文件在`C:\Users\61772\.ssh`
- 如果是首次生成则忽略这步

## 3 生成秘钥

- 在git命令框中执行下面命令

    ~~~
    ssh-keygen -t rsa -C "your@email.com"
    ~~~

    > 注：请填你设置的邮箱地址  

- 一路yes和回车，然后系统会自动在.ssh文件夹下生成两个文件，id_rsa和id_rsa.pub

## 4 在 Github/Gitee 中添加秘钥
- 用记事本打开 id_rsa.pub 将全部的内容复制
- 打开 Github/Gitee →进入设置→进入ssh设置→点击添加秘钥，然后将刚刚复制的粘贴进去就可以了