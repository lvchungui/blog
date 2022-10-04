---
title: VScode中上传到Gitee或Github
categories: 
- 技术

tags:
- VScode
- Github
- Gitee
---


1. 先把Gitee或Gihub的仓库克隆到本地
2. 在VScode中打开克隆过来的文件夹，先暂存后提交，最后同步更新即可  
3. 使用VSCode中报错信息：Git installation not found 解决方法

   ![图 5](../images/ff9a6633df31b7281fca932bc889d5170b76a56e2fc1762c25d37fa7f96b01c7.png)  

   - 设置→输入命令“git.path”→点击“在settings.json中编辑”

      ![图 6](../images/0480e70d8820102e78ddf38cfcd989356fdaeab6c43dea384e9c72167f4b10e7.png)  

      ![图 7](../images/9789b9834c93b1b6b448d3bf2b3503d84e48490c8daf5331abd5cecbb87841c6.png)  

   - 添加Git的安装地址，在git.path那里输入我们git的安装地址：注意分隔符为“/”,而不是“\”

      ![图 8](../images/bfbed60bcbc01b4b18cfb234fa34cd5c7e27fc44b253a2490800b027b625e4b6.png) 

   - 重启VScode即可