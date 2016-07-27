---
title: Hexo 搭建一步一步github博客
date: 2016-07-27 22:38:45
tags:
---
Hexo是基于nodejs的一个快速简洁高效的博客框架，这篇文章将要介绍如何如何利用Github Pages免费静态站点托管服务、Hexo博客框架来建立个人在github上的博客站点。本文版本是Hexo3.2.2。       
## 一、安装相关软件
这一点[Hexo官方文档](https://hexo.io/zh-cn/docs/#安装)上面写得很清晰了，直接复制下来,稍微补充了一点内容：    
### 安装 Git
- Windows：下载并安装 git.
- Mac：使用 Homebrew, MacPorts 或下载 安装程序 安装。
- Linux (Ubuntu, Debian)：sudo apt-get install git-core
- Linux (Fedora, Red Hat, CentOS)：sudo yum install git-core
### 安装 Node.js
window下，到官方网站下载nodejs的安装包即可。   
Linux下安装 Node.js 的最佳方式是使用 nvm。

cURL:
```
$ curl https://raw.github.com/creationix/nvm/master/install.sh | sh
```
Wget:
```
$ wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
```
安装完成后，重启终端并执行下列命令即可安装 Node.js。
```
$ nvm install 4
```
或者您也可以下载 安装程序 来安装。

### 安装 Hexo
所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。
```
$ npm install -g hexo-cli
```

## 二、使用Hexo建立本地站点
### 1.初始化及运行
打开命令行cd到某一目录，然后运行下面的命令就可以初始化Hexo站点需要的东西
```
hexo init <folderName>
```
等初始化完成后，就可以看到里面已经多了一些文件夹和文件。
可以通过命令行进入该文件夹，运行hexo看看效果：
```
cd <folderName>
hexo server -p 5000  //指定5000端口
```
通过浏览器访问`http://localhost:5000`就可以看到hexo默认的页面了。

### 2.修改配置
hexo的配置文件是站点根目录下的`_config.yml`，里面可以配置博客的大部分内容

参数 | 描述
--- | ---
title | 网站标题
subtitle | 网站副标题
description | 网站描述
author | 您的名字
language | 网站使用的语言
timezone | 网站时区。Hexo默认使用您电脑的时区。时区列表。比如说：America/New_York, Japan, 和 UTC 。

具体见[官网的配置](https://hexo.io/zh-cn/docs/configuration.html)一节   
**注意：配置的时候，每一项的key的冒号`:`后面要留一个空格，不然会报错**。















【参考文档】    
https://xuanwo.org/2015/03/26/hexo-intor/       
https://hexo.io/zh-cn/docs/setup.html