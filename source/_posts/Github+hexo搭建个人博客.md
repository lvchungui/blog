---
title: Github+hexo搭建个人博客
categories: 
- 其他
tags:
- hexo
---

## 1 环境安装

1. 下载安装：[node.js](https://nodejs.org/zh-cn/download/)
2. 安装 hexo
    ~~~py
    npm install -g hexo-cli
    ~~~
3. 在一个空文件夹里初始化hexo
    ~~~py
    hexo init
    ~~~
4. 本地预览 hexo 使用以下命令，浏览器打开 http://localhost:4000 就可以看到hexo的初始界面了
    ~~~py
    hexo s      #本地预览
    ~~~


## 2 主题安装

1. 安装 ayer 主题（如果想要安装其他主题到 [hexo官方主题库](https://hexo.io/themes/) 寻找即可）
    ~~~py
    npm i hexo-theme-ayer -S
    ~~~
2. 将博客根目录下的 `_config.yml` 里的 `theme` 值修改成 `ayer`
3. 主题配置：找到 `ayer` 主题目录下的 `_config.yml` 文件自行配置


## 3 插件安装

### 搜索

~~~py
npm install hexo-generator-searchdb --save
~~~
安装完成后将以下配置复制到你博客根目录下的 `_config.yml` 里（注意不是 `ayer` 目录下的）:
~~~py
# hexo-generator-searchdb
search:
path: search.xml
field: post
format: html
~~~

### 分类

~~~py
hexo new page categories
~~~
安装完成后找到 `/source/categories/index.md` 文件，默认内容如下：
~~~py
---
title: categories
date: 2022-10-02 14:35:38
---
~~~
在上面内容后面添加两行代码，添加后的内容如下：
~~~py
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
~~~py
---
title: Github+hexo搭建个人博客
categories: 
- 其他
---
~~~

### 标签

~~~py
hexo new page tags
~~~
安装完成后找到 `/source/tags/index.md` 文件，默认内容如下：
~~~py
---
title: 标签
date: 2022-10-02 15:11:19
---
~~~
在上面内容后面添加两行代码，添加后的内容如下：
~~~py
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
~~~py
---
title: Github+hexo搭建个人博客
categories: 
- 其他
tags:
- hexo
---
~~~

### 相册

~~~py
hexo new page photos
~~~
然后将以下内容复制到 `/source/photos/index.md` 文件，`img_url` 替换成图片路径，`caption` 替换成图片名称：
~~~py
---
title: Gallery

albums: [["img_url", "img_caption"], ["img_url", "img_caption"]]
---
~~~
最后在 `ayer` 目录下的 `_config.yml` 里的 `menu` 下添加 `相册: /photos` 即可


### 二次元看板娘

~~~py
npm install --save hexo-helper-live2d
~~~
然后将以下配置复制到你博客根目录下的 `_config.yml` 里（注意不是 `ayer` 目录下的）:
~~~py
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
~~~py
model:
    use: live2d-widget  ## 模型文件
~~~


## 4 部署在Github/Gitee

1. 安装`git`部署插件
  ~~~py
  npm install --save hexo-deployer-git
  ~~~
2. 修改配置文件`_config.yml`，填上仓库的地址(这里我是部署在Gitee)
  ~~~py
  deploy:
    type: git
    repository: https://gitee.com/lvchungui/lvchungui.git
    branch: master
  ~~~
3. 