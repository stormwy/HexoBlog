---
title: 使用Hexo一步一步搭建github博客
date: 2016-07-28 14:03:39
categories: Nodejs
tags: Hexo 
---
Hexo是基于Nodejs的一个快速简洁高效的博客框架，这篇文章将要介绍如何使用Hexo博客框架、Github Pages免费静态站点托管服务来建立个人在github上的博客站点。本文版本是Hexo 3.2.2。       
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
我运行的是：`hexo inti HexoBlog`        
等初始化完成后，就可以看到生成了一个名字为`HexoBlog`的文件夹,打开该文件夹，可以看到Hexo生成的博客框架文件。
可以通过命令行进入该文件夹，运行hexo服务器看看初始化完成的效果：
```
cd <folderName>
hexo server -p 5000  //指定5000端口
```
通过浏览器访问`http://localhost:5000`就可以看到hexo默认的页面了。

### 2.修改配置
hexo的配置文件是站点根目录下的`_config.yml`，里面可以配置博客的大部分内容   
下面是常用配置：		

| 参数                | 描述                                       |
| ----------------- | ---------------------------------------- |
| title             | 网站标题                                     |
| subtitle          | 网站副标题                                    |
| description       | 网站描述，用于标识网站内容，被搜索引擎收录的简要网站描述。            |
| author            | 您的名字                                     |
| language          | 网站使用的语言,设置为“zh-CN”,主题的语言是在这里设置。          |
| url               | 网址                                       |
| root              | 网站根目录                                    |
| theme             | 当前主题名称。值为false时禁用主题                      |
| post_asset_folder | 启动[资源](https://hexo.io/zh-cn/docs/asset-folders.html)文件夹,用来管理文章的图片等资源文件，建议设置为`true` |
| deploy            | 部署部分的设置，请看本文第三节                          |

其他配置具体见官网的[配置](https://hexo.io/zh-cn/docs/configuration.html)一节   
**注意：配置的时候，每一项的key的冒号`:`后面要留一个空格，不然会报错**。

### 3.写文章
#### 文章创建
首先是先创建一篇新文章      
`hexo new [layout] <title>`     
layout是文章布局，title是文章标题。如果不指定layout，则使用默认layout。     
例子：  
`hexo new "使用Hexo一步一步搭建github博客"`        
运行完成后，将会在博客根目录`HexoBlog`的`\source\_posts`目录底下生成`使用Hexo一步一步搭建github博客.md`文件。        
打开这个md文件，可以看到下面的内容      
```
---
title: Hexo一步一步搭建github博客
date: 2016-07-27 22:38:45
tags:
---
```
这上面的内容是文章的配置，详细说明可以见官网[Front-matter](https://hexo.io/zh-cn/docs/front-matter.html)一节;
我们可以用[markdown](http://sspai.com/25137)语法，在默认内容的下面写自己文章的内容即可。

#### 图片插入
图片插入可以使用本地图片或者网络图片，使用网络图片，用markdown语法写入即可，图床可以用这个网站:[极简图床](http://yotuku.cn/),这个图床可以用网站提供的公共空间存储图片，或者上传图片到自己的[七牛云储存（免费用户有10G的空间）](http://www.qiniu.com/feature)        

当然,用自己本地的图片是最安全的，这就要通过Hexo的[资源文件夹](https://hexo.io/zh-cn/docs/asset-folders.html)实现了。我将官网的资源文件夹使用简单说明一下：     
- 设置`config.yml`的`post_asset_folder`为`true`，开启资源文件夹功能

- 通过相对路径标签引用资源，而不是markdown语法引用。      
  {\% asset_img 1.png [title] \%}     

  上面的“\”要去掉，这里因为是hexo的指令，不能直接显示在文章里，所以这里才加上。


### 4.发布文章、运行
写好文章后，我们通过下面的命令将文字编译成静态html等资源文件：      
`hexo generate`     
运行后，博客根目录下就会生成`public`站点文件夹，里面是编译生成的文件。这时候，我们可以运行或者重启hexo查看效果      
```
hexo server //这样启动，默认端口为4000  
```
然后访问`http://localhost:4000`，就可以看到刚才写的文章了。


## 三、将Hexo博客站点部署到github Page
[Github Page](https://pages.github.com/)是github提供的静态站点服务，在github创建`userName.github.io`的仓库，将静态html文件上传到该仓库，就可以通过`https://userName.github.io`进行访问了，具体设置见：https://pages.github.com/           

HexoBlog部署到git我们需要安装`hexo-deployer-git`插件，在博客HexoBlog根目录运行：     
`npm install hexo-deployer-git --save`      
然后修改`_config.yml`中的`deploy`配置：     
```
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
```
参数说明:
		
参数 | 描述
--- | ---
type | 部署方式（git/heroku/rsync/openshift/ftpsync）
repo | 库（Repository）地址
branch | 分支名称。如果您使用的是 GitHub 或 GitCafe 的话，程序会尝试自动检测。	


设置好部署参数之后，通过hexo的部署指令，就可以一键部署了：      
```
hexo deploy
```


实际上，我们也可以手动将`public`文件夹的内容，上传到`userName.github.io`，完成部署，这个就不说了。



## 四、Hexo进阶使用
### 更换主题
目前本博客用的是[屠城9441](https://www.haomwei.com/technology/maupassant-hexo.html)的博客主题[maupassant-hexo](https://github.com/tufu9441/maupassant-hexo)	

Hexo主题更换很容易，首先到https://hexo.io/themes/ 里面寻找你喜欢的主题，然后进入该主题的链接，里面一般有文章介绍从哪里获取主题文件，或者直接到github里面按照`hexo+主题关键字搜索`，找到主题关键字之后，`git clone`下载到本地。然后将`maupassant`文件夹复制一份到博客根目录的`themes`里面，最后修改`_config.yml`的`theme`值为`主题名`即可，这里是修改为`maupassant`。		

不过`maupassant`主题有点特别，还需要依赖`hexo-renderer-jade`和`hexo-renderer-sass`，所以还要安装两个插件		

```
npm install hexo-renderer-jade --save
npm install hexo-renderer-sass --save
```

安装完成后，先清理一遍原来编译的静态资源文件，然后重新生成，最后运行hexo，就可以看到新主题的博客啦。

```
hexo clean 
hexo generate
hexo server
```


【参考文档】    
https://hexo.io/zh-cn/docs      
https://xuanwo.org/2015/03/26/hexo-intor/	
https://www.haomwei.com/technology/maupassant-hexo.html