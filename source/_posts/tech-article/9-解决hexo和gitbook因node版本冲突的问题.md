---
title: 解决Hexo和Gitbook因node版本冲突的问题
categories: 
- 技术
tags:
- Gitbook
- Hexo
- Node
---

- 问题：由于gitbook要在低版本的node下运行，而hexo则需要在高版本的node下运行，所以同时使用hexo和gitbook时难免会发生冲突。使用高版本的node时，使用gitbook执行命令时会出现以下错误
    ~~~py
    C:\Users\61772\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules\graceful-fs\polyfills.js:287
    ~~~
- 解决方法：
    1. 按住Ctrl左击上面的路径会打开一个js文件
    2. 找到文件的62、63和64行，把有函数名`statstatFix`的这三行注释掉即可

        ![图 1](../images/9900c370561e3c988f2a8dd5601f4dcfb29765aec9a5eb21607cacbe0b1d56f5.png)  



