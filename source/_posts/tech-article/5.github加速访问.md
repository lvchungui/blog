---
title: Github加速访问
categories: 
- 技术

tags:
- Github
---


## 1 软件介绍

- github加速神器：FastGithub
- 开源项目地址：https://github.com/dotnetcore/FastGithub

## 2 软件功能

- 解决github打不开、用户头像无法加载、releases无法上传下载、git-clone、git-pull、git-push失败等问题
- 提供域名的纯净IP解析
- 提供IP测速并选择最快的IP
- 提供域名的tls连接自定义配置
- google的CDN资源替换，解决大量国外网站无法加载js和css的问题

## 3 软件下载

- 主链接：https://github.com/dotnetcore/fastgithub/releases
- 备用链接：https://pan.baidu.com/s/1ewHysiOaGsPH0yttFEVrvA?pwd=4qrh 

## 4 软件的使用

- Windows-x64桌面：双击运行FastGithub.UI.exe

## 5 证书验证问题

### 5.1 Git

- 相关问题：git操作提示`SSL certificate problem`
- 解决方法：需要关闭git的证书验证，在git的命令框中输入：`git config --global http.sslverify false`

### 5.2 火狐浏览器

- 相关问题：firefox提示连接有潜在的安全问题
- 解决方法：设置→隐私与安全→证书→查看证书→证书颁发机构，导入`fastgithub.cer`文件（这个文件在cacert文件夹下），然后勾选“信任由此证书颁发机构来标识网站”


