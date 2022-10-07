---
title: Github/Gitee+hexo搭建个人博客
categories: 
- 技术
tags:
- Hexo
---

## 1 环境安装

1. 下载安装：[node.js](https://nodejs.org/zh-cn/download/)
2. 安装 hexo
    ~~~
    npm install -g hexo-cli
    ~~~
3. 在一个空文件夹里初始化hexo
    ~~~
    hexo init
    ~~~
4. 本地预览 hexo 使用以下命令，浏览器打开 http://localhost:4000 就可以看到hexo的初始界面了
    ~~~
    hexo s      #本地预览
    ~~~


## 2 主题安装

1. 安装 ayer 主题（如果想要安装其他主题到 [hexo官方主题库](https://hexo.io/themes/) 寻找即可）
    ~~~
    npm i hexo-theme-ayer -S
    ~~~
2. 将博客根目录下的 `_config.yml` 里的 `theme` 值修改成 `ayer`
3. 主题配置：找到 `ayer` 主题目录下的 `_config.yml` 文件自行配置


## 3 插件安装

### 搜索

~~~
npm install hexo-generator-searchdb --save
~~~
安装完成后将以下配置复制到你博客根目录下的 `_config.yml` 里（注意不是 `ayer` 目录下的）:
~~~
# hexo-generator-searchdb
search:
path: search.xml
field: post
format: html
~~~

### 分类

~~~
hexo new page categories
~~~
安装完成后找到 `/source/categories/index.md` 文件，默认内容如下：
~~~
---
title: categories
date: 2022-10-02 14:35:38
---
~~~
在上面内容后面添加两行代码，添加后的内容如下：
~~~
---
title: categories
date: 2022-10-02 14:35:38
type: "categories"
layout: "categories"
---
~~~
① 文章分类：打开需要添加分类的文章，在开头为其添加 `categories` 属性
② `categories: - 其他`表示添加这篇文章到 `其他` 这个分类
③ 注意：hexo一篇文章只能属于一个分类，也就是说如果在 `- 其他` 下方添加 `- xxx`，hexo不会产生两个分类，而是把分类嵌套（即该文章属于 `- 其他` 下的 `-xxx` 分类）
~~~
---
title: Github+hexo搭建个人博客
categories: 
- 其他
---
~~~

### 标签

~~~
hexo new page tags
~~~
安装完成后找到 `/source/tags/index.md` 文件，默认内容如下：
~~~
---
title: 标签
date: 2022-10-02 15:11:19
---
~~~
在上面内容后面添加两行代码，添加后的内容如下：
~~~
---
title: 标签
date: 2022-10-02 15:11:19
type: "tags"
layout: "tags"
---
~~~
① 添加标签：打开需要添加分类的文章，在开头为其添加 `tags` 属性
② `tags: - hexo`表示为这篇文章添加 `hexo` 这个标签
③ 点击首页的`标签`可以看到该标签下的所有文章
~~~
---
title: Github+hexo搭建个人博客
categories: 
- 其他
tags:
- hexo
---
~~~

### 相册

~~~
hexo new page photos
~~~
然后将以下内容复制到 `/source/photos/index.md` 文件，`img_url` 替换成图片路径，`caption` 替换成图片名称：
~~~
---
title: Gallery

albums: [["img_url", "img_caption"], ["img_url", "img_caption"]]
---
~~~
最后在 `ayer` 目录下的 `_config.yml` 里的 `menu` 下添加 `相册: /photos` 即可


### 二次元看板娘

~~~
npm install --save hexo-helper-live2d
~~~
然后将以下配置复制到你博客根目录下的 `_config.yml` 里（注意不是 `ayer` 目录下的）:
~~~
live2d:
  enable: true  # 是否启动
  scriptFrom: local # 默认
  pluginRootPath: live2dw/  # 插件在站点上的根目录(相对路径)
  pluginJsPath: lib/  # 脚本文件相对与插件根目录路径
  pluginModelPath: assets/  # 模型文件相对与插件根目录路径
  tagMode: false  # 标签模式, 是否仅替换 live2d tag标签而非插入到所有页面中
  debug: false  # 调试, 是否在控制台输出日志
  model:
    use: live2d-widget  ## 模型文件
  display:
    position: right # 定位方向 left right top bottom
    width: 150  # 小人宽度
    height: 300 #  小人高度
    hOffset: -15  # 向 偏移
    vOffset: -15  # 像 偏移
  mobile:
    show: true  # 手机端是否显示
  react:
    opacity: 0.7  # 模型透明度
~~~
① [下载模型](https://huaji8.top/post/live2d-plugin-2.0/)，在里面找到自己喜欢的一款模型然后下载即可，比方说作者喜欢的是 `koharu` 这个模型，那么就使用 `npm install --save live2d-widget-model-koharu` 进行安装
② 安装后我们在 `node_modules` 目录下面找到 `live2d-widget-model-koharu` 这个文件夹，把这个文件夹复制在我们的hexo博客的根目录(因为我们是在根目录的 `_config.yml` 里添加的配置)
③ 最后我们打开添加的配置文件，找到下面这行，把use后面改成我们刚才复制过来的文件夹的名称即可
~~~
model:
    use: live2d-widget  ## 模型文件
~~~
更多插件可以在[hexo官方插件库](https://hexo.io/plugins/)里查找

## 4 部署在Github/Gitee

1. 安装`git`部署插件
  ~~~
  npm install --save hexo-deployer-git
  ~~~

2. 在配置文件`_config.yml`下分别修改以下内容（我这里是部署在Gitee上，部署在Github同理）
  ~~~
  url:  https://lvchungui.gitee.io # 仓库使用page服务后的网址
  root: /
  ~~~
  ~~~
  deploy:
    type: git
    repository: https://gitee.com/lvchungui/lvchungui.git # 仓库的地址
    branch: master # 要上传的分支
  ~~~
  注意：仓库的网址和地址一定要对应

3. 最后依次执行以下命令即可
  ~~~
  hexo c # 清除缓存文件 (db.json) 和已生成的静态文件 (public)
  hexo g # 生成静态文件
  hexo d # 部署网站
  # hexo g 和 hexo d 可以合并写成 hexo g -d
  ~~~
  可能遇到的问题：'git' 不是内部或外部命令，也不是可运行的程序
  [解决方法](https://www.cnblogs.com/ldq678/p/13287924.html)：找到git的安装目录→打开系统环境变量→在用户变量和系统变量下的Path中新建一个→然后把git的安装目录的路径复制进去即可

## 5 图片不显示问题

- 资源(Asset)代表source文件夹中除了文章以外的所有文件，例如图片、CSS、JS文件等。比方说，如果你的Hexo项目中有图片，那最简单的方法就是将它们放在`source/images` 文件夹中。然后通过类似于`![](/images/image.jpg）`的方法访问它们


## 6 绑定域名

1. 购买一个域名（我这里使用腾讯云做个示范）
2. 进入腾讯云→点开我的域名→点击解析

    ![图 1](../images/14e2a7269aea8c27311fee1d04ede690d948ac65e2dc33905a2ba4b8b250bc48.png)  

3. 如图所示，添加两条记录（记录值是你的博客网址）

    ![图 2](../images/a6ddc94d4d4cda83ffc91ca54997724bf0cbcd40f8cd6136cca7bc4df29c4536.png)  

4. 打开博客仓库→点击page服务→绑定域名

    ![图 3](../images/b7b0d55a8109b23eabc0510f7001fa0dec8a839c135412a8aa1b2d2416951ad1.png)  

