---
title: Gitbook搭建个人笔记
date: 2022-10-01 14:35:38
categories: 
- 技术
tags:
- Gitbook
---

## 1 环境准备

###  配置 Node.js 环境

- 下载安装 Node.js，由于目前 Gitbook 项目已经停止维护，Node 过高可能出现不兼容问题。目前，Node 版本 10.# 以下版本可使用，这里给出 Node 版本 10.# 的下载链接：https://pan.baidu.com/s/1TIaieryRGJplVBd-nH8SDA?pwd=yu5h
- 安装成功后，打开 cmd 执行命令可查看 node 版本和 npm 版本
  - 查看node版本：node -v
  - 查看npm版本：npm -v

###  安装 Gitbook

- 打开 cmd 执行下面命令，安装 gitbook

    ~~~c
    npm install -g gitbook-cli
    ~~~

## 2 搭建个人笔记

###  Gitbook 初始化

- 创建一个文件夹，并进入到该文件夹中，执行下面命令，初始化 gitbook 

    ~~~c
    gitbook init
    ~~~

- 命令执行完成之后可以看到创建了 `SUMMARY.md` 文档，这是笔记的目录文档；还有一个 `REAMDE.md` 文档，是用来对这个笔记进行介绍

###  npm 初始化

- 执行下面命令，初始化 npm

    ~~~c
    npm init
    ~~~

- 命令会提示输入项目信息，可默认不填写，直接回车。最后，会显示配置信息，输入yes回车即可初始化完毕
- 初始化成功后，系统会自动在当前目录创建`package.json`文件，这是 npm 的配置文件

###  配置脚本命令

**配置启动脚本命令**

- 在`package.json`文件的`scripts`中配置如下的脚本命令

    ~~~js
    "scripts": {
        "serve": "gitbook serve",
        "build": "gitbook build"
    }
    ~~~

- 上面分别是 gitbook 在本地启动的命令，和 gitbook 打包成 HTML 静态文件的命令
- 对于本地显示笔记，我们可以直接通过下面命令启动，启动成功后，就可以在浏览器输入 http://localhost:4000/ 查看自己的笔记，`gitbook build`命令后面再介绍 

    ~~~c
    gitbook serve
    ~~~

**配置插件脚本命令**

- 在文件夹的根目录中创建一个`book.js`的文件，并在该文件中配置如下信息

    ~~~js
    module.exports = {
        // 书籍信息
        title: '书名',
        description: '描述',
        isbn: '图书编号',
        author: '作者',
        lang: 'zh-cn',

        // 插件列表
        plugins: [],

        // 插件全局配置
        pluginsConfig: {},

        // 模板变量
        variables: {
            // 自定义
        },
    };
    ~~~

- 在后面安装插件的时候需要在`book.js`文件中填入相关信息

###  安装插件

Gitbook 最灵活的地方就是有很多插件可以使用，当然如果对插件不满意，也可以自己写插件。所有插件的命名都是以gitbook-plugin-xxx的形式，gitbook 插件地址：https://www.npmjs.com/

####  搜索插件

- 在命令行输入下面命令安装搜索插件search-pro，这个插件可以搜索任何字符并在 GitBook 中突出显示它

    ~~~c
    npm install gitbook-plugin-search-pro
    ~~~

- 安装完成之后会多出一个`node_modules`的文件夹，这个文件夹是专门存放插件的，以后下载的插件都会存放在这个文件里
- 插件安装成功后，还要在`book.js`中的`plugins`里添加如下插件的配置。- 号代表禁用插件，如果新安装的插件和gitbook自带的插件冲突了，需要禁用自带的插件才能使用新安装的；没有冲突的话直接在`plugins`里加上插件的名字就行

    ~~~js
    plugins: ["-lunr","-search","search-pro"],
    ~~~

####  代码插件

- 在命令行输入下面命令安装代码插件code，这个插件可以在 GitBook 中显示代码和代码行号

    ~~~c
    npm install gitbook-plugin-code
    ~~~

- 插件安装成功后，还要在`book.js`中的`plugins`里添加如下插件的配置

    ~~~js
    plugins: ["-lunr","-search","search-pro","code"],
    ~~~

####  菜单折叠插件

- 在命令行输入下面命令安装菜单折叠插件expandable-chapters，这个插件可以对 GitBook 左侧中的目录进行折叠操作

    ~~~c
    npm install gitbook-plugin-expandable-chapters
    ~~~

- 插件安装成功后，还要在`book.js`中的`plugins`里添加如下插件的配置

    ~~~js
    plugins: ["-lunr","-search","search-pro","code","expandable-chapters"],
    ~~~

####  返回顶部插件

- 在命令行输入下面命令安装返回顶部插件back-to-top-button，这个插件可以对 GitBook 左侧中的目录进行折叠操作

    ~~~c
    npm install gitbook-plugin-back-to-top-button
    ~~~

- 插件安装成功后，还要在`book.js`中的`plugins`里添加如下插件的配置

    ~~~js
    plugins: ["-lunr","-search","search-pro","code","expandable-chapters","back-to-top-button"],
    ~~~

####  主题插件

- 在命令行输入下面命令安装lou主题插件，这个主题插件是我目前用到最好的一款

    ~~~c
    npm install gitbook-plugin-theme-lou
    ~~~

- 插件安装成功后，还要在`book.js`中添加如下插件的配置

    ~~~js
    // book.js 
    { 
        "plugins" :  [ "theme-lou" ] , 
        "pluginsConfig" :  { 
            "theme-lou" :  { 
                "color" :  "#FF4848" ,  // 主题色 
                "favicon" :  "static/favicon.ico" ,  // favicon图标 
                "logo" :  "static/logo.png" ,  // 顶部左侧图标 
                "appleTouchIconPrecomposed152" :  "static/apple.png" ,  // apple图标 
                "copyrightLogo" :  "assets/copyright.png" ,   // 底部水印LOGO 
                "forbidCopy" :  true ,  // 页面是否禁止复制 
                "search-placeholder" :  "Input Keywords to Search" ,  // 搜索框默认文本 
                "book-summary-title" :  "Article Directory" ,  // 目录标题 
                "book-anchor-title" :  "Search In the Article" ,  // 本章目录标题 
                "hide-elements" :  [ ".summary .gitbook-link" ,  ".summary .divider" ] ,  // 需要隐藏的标签 
                "copyright" :  { 
                    "author" :  "松露老师"   // 底部版权展示的作者名 
                } 
            } 
        } , 
        "variables" :  { 
            "themeLou" :  { 
            // 顶部导航栏配置 
                "nav" :  [ 
                    { 
                    "target" :  "_blank" ,  // 跳转方式: 打开新页面 
                    "url" :  "http://..." ,   // 跳转页面 
                    "name" :  "简易教程"   // 导航名称 
                    } 
                ] , 
                // 底部打赏配置 
                "footer" :  { 
                    "donate" :  { 
                    "button" :  "捐赠" ,  // 打赏按钮 
                    "avatar" :  "头像地址" ,  // 头像地址 
                    "nickname" :  "松露老师" ,  // 昵称 
                    "message" :  "随意打赏，但不要超过一顿早餐钱！" ,  // 打赏消息文本 
                    "text" :  "『 赠人玫瑰 🌹 手有余香 』" ,  // 打赏话语 
                    "wxpay" :  "你的微信收款码地址" ,  // 微信收款码 
                    "alipay" :  "你的支付宝收款码地址"  // 支付宝收款码 
                    } , 
                    "copyright" :  true  // 是否显示版权 
                } 
            } 
        } 
    } 
    ~~~

###  目录配置

- GitBook 使用文件 `SUMMARY.md` 来定义书本的章节和子章节的结构，文件 `SUMMARY.md` 被用来生成书本内容的预览表
- `SUMMARY.md` 的格式是一个简单的链接列表，链接的名字是章节的名字，链接的指向是章节文件的路径，格式如下所示

    ~~~c
    - [章节一](chapter1.md)
    - [章节二](chapter2.md)
    - [章节三](chapte#d)
    ~~~
    ~~~c
    - [第一章](part1/README.md)
      - [1.1 第一节](part1/writing.md)
      - [1.2 第二节](part1/gitbook.md)
    - [第二章](part2/README.md)
      - [2.1 第一节](part2/feedback_please.md)
      - [2.2 第二节](part2/better_tools.md)
    ~~~

###  额外设置

- 由于这个主题右侧的目录会显示1~6级标题，而我不想显示1级标题，需要进行以下设置
- 找到`lou.js`文件，把`.find`里的h1去掉即可，如下图所示。文件路径：`node_modules\gitbook-plugin-theme-lou\_assets\lou.js`

    ![图 1](../images/a474cad45c7ddfed6be4f491c2f29a95887e85907bc4e599fa19f68b22095a65.png)  



## 3 服务器部署

这里推荐使用Github Page，因为Gitee Page 每次提交代码后还要手动更新部署，而Github Page 提交代码后会自动部署

### Gitee Page

- 在命令行输入下面命令构建项目，成功后即可在_book文件夹中生成对应的静态网页资源

    ~~~c
    gitbook build
    ~~~

    ~~~c
    执行命令 gitbook build 出现的问题及解决方法

    问题：npm报错：无法加载文件 **.ps1，因为在此系统上禁止运行脚本
    解决方法：在命令行依次执行如下命令
        1. 获取有效的执行策略：Get-ExecutionPolicy 
        2. 更改当前用户执行策略：Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    ~~~

- 在 gitee 上新建一个仓库，把整个文件夹全部上传到仓库里
- 点击仓库→点击服务→点击 Gitee pages

    ![图 1](../images/3e11efbb6c4524dd2e0a165903e1be4f515a7d75f4cfc048dff04a90bc5ae0c0.png)  

    ![图 2](../images/05a4fbb9285610cf64cc9bfa2d4f7bffd4559877b9f206c00484d28cca3affec.png)  


### Github Page

由于 Github Page 在部署目录的时候只能选择根目录或者`docs`目录，为了方便部署，我选择用`docs`目录部署。所以在本地`gitbook build`的操作会和之前有所不一样，按照下面的步骤执行即可


- 由于执行`gitbook build`命令会默认在`_book`文件中生成对应的静态网页资源，而我们得在`docs`文件夹内生成对应的静态网页资源，所以在命令行输入下面命令构建项目，成功后即可在docs文件夹中生成对应的静态网页资源

    ~~~c
    gitbook build ./ ./docs
    ~~~

    ~~~c
    参数一，书籍所在的目录，如果执行build指令时位于当前项目目录，输入./
    参数二，输出的目录，相对于当前目录
    ~~~

    ~~~c
    执行命令 gitbook build ./ ./docs 出现的问题及解决方法

    问题：Error: ENOENT: no such file or directory, open 'D:\Repositories\gitbook\_book\gitbook\gitbook-plugin-theme-lou\logo.png'
    解决方法：找到index.js文件，把里面的_book改成docs。文件路径： node_modules\gitbook-plugin-theme-lou\index.js
    ~~~

    ![图 2](../images/41cf5fba8e6a31f5052b0e5fc209af73cf04531067b278103c00aa2f8b45d162.png)  

- 在 github 上新建一个仓库，把整个文件夹全部上传到仓库里
- 点击仓库的设置→点击pages，按照下图设置即可

    ![图 3](../images/77ba37fd9dba0d1bdb31557bea072ed93036449bdc056f123af44cadbae83523.png)  


