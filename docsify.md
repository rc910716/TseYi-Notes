# docsify搭建

**Docsify** 是一款轻量级的文档生成工具，能够快速将 Markdown 文件转化为动态文档网站。与传统的静态生成工具（如 GitBook）不同，Docsify 不会生成静态 HTML 文件，而是通过运行时动态加载和渲染 Markdown 文件。

1. 到官网下载Node.js和npm（[Node.js — 下载 Node.js®](https://nodejs.org/zh-cn/download)）

2. 然后进行一些初始化操作

   ```shell
   #全局安装 Docsify CLI 工具
   npm i docsify-cli -g
   
   #安装完成后，使用以下命令初始化项目：
   docsify init ./docs
   
   #运行以下命令启动本地服务器，默认访问地址为 http://localhost:3000：
   docsify serve docs
   
   ```

   