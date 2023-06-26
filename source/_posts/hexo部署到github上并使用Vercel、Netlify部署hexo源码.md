---
title: hexo部署到github上并使用Vercel、Netlify部署hexo源码
categories:
- 教程
cover: https://pic.rmb.bdstatic.com/bjh/ffdbc82d6af46391557ccbf913f5b7c5.jpeg
date: '2023-06-26 07:38:53'
summary: 真的非常简单( ˃̶̤́ ꒳ ˂̶̤̀ )
tags:
  - 教程
  - Hexo
  - 主題
  - butterfly
toc: true
sticky: 100
---
## 前言

注意，这篇文章篇幅较长，主要针对新手，每一步很详细，所以可能会显得比较啰嗦，所以建议基础比较好小伙伴根据目录选择自己感兴趣的部分跳着看✧٩(ˊωˋ*)و✧

> 将源码部署到github

## 安装

### 安装git
**linux**
```Bash
apt-get update
apt install git-core -y
```
**windows**
去官网下载并打开以后按照安装程序使用

**检查是否安装成功**
```
git -v
```
### 安装nodejs（以14.x为例)
**linux**
```Bash
curl -sL https://deb.nodesource.com/setup_14.x | bash  - 
sudo apt install nodejs
```
**windows**
去官网下载并打开以后按照安装程序使用

**检查是否安装成功**

```
node -v
npm -v
```

### 安装hexo

```
npm install hexo-cli -g
```

## 搭建

```
hexo init MyBlog //也可以用其他文件夹
cd MyBlog
```

测试

```Bash
hexo g && hexo s
```

用浏览器打开[https://localhost:4000/](https://localhost:4000/)
看到如下图就是成功了
![效果](https://pic.rmb.bdstatic.com/bjh/9f4a6a09b5b3f6516668ab45827cc574.png)
按`ctrl+c`关闭本地服务器。

## GitHub配置

### 注册Github账号创建个人仓库

接下来就去注册一个`github`账号，用来存放我们的网站。大多数小伙伴应该都有了吧，作为一个合格的程序猿（媛）还是要有一个的。
打开[https://github.com/](https://github.com/)，新建一个项目仓库`New repository`，如下所示：
![github配置](https://pic.rmb.bdstatic.com/bjh/ba46323db6dbccc9d1f923e2569daa92.jpeg)
然后如上图所示，输入自己的账号名字，后面一定要加.github.io后缀，README初始化也要勾。

### 将hexo部署到GitHub
先将仓库主分支复制成另一个分支，再将hexo源代码复制到github中

打开博客根目录下的_config.yml文件，这是博客的配置文件，在这里你可以修改与博客配置相关的各种信息。<br/>
修改最后一行的配置：

```yml
deploy:
  type: git
  repository: https://github.com/yourname/yourname.github.io
  branch: master
```

repository修改为你自己的github项目地址即可，就是部署时，告诉工具，将生成网页通过git方式上传到你对应的链接仓库中。

```Bash
"hexo-deployer-git": "^3.0.0",
```


## 写文章、发布文章

新建一篇文章在自己的仓库里，配置如下
```
---
title:
date:
tags:
  - 
categories:
description:
cover:
comments:
---
```
## 个性化

在文件根目录下的`_config.yml`，就是整个hexo框架的配置文件了。可以在里面修改大部分的配置。详细可参考官方的[配置描述](https://hexo.io/zh-cn/docs/configuration)。

```Yml
# Site
title: Hexo #网站名字
subtitle: '' #网站副标题
description: '' #网站描述
keywords:
author: John Doe #你的名字
language: en #网站使用的语言
timezone: '' #网站时区
# URL
## 如果您的网站位于子目录中，请将url设置为'https://yoursite.com/child'，将root设置为'/child/'
url: https://yoursite.com #可以改成你的github.io网址
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
pretty_urls:
  trailing_index: true # 设置为false时会将末尾的index.html去掉
  trailing_html: true # 设置为false时会将末尾的.html去掉，对index.html无效
```
## 博客部署

## 更多玩法

### 更改主题
```Yml
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: butterfly
```

### 安装插件
因为我们的博客部署到github上，所以我们可以通过将插件安装**package.json**，那么插件怎么安装到github博客源代码
```Yml
    "插件名称": "^插件版本"，
```
例如我自己用的package.json
```Yml
  "dependencies": {
    "aplayer": "^1.10.1",
    "hexo": "^5.0.0",
    "hexo-abbrlink": "^2.2.1",
    "hexo-butterfly-swiper-marcus": "^1.0.7",
    "hexo-butterfly-footer-marcus": "^1.1.3",
    "hexo-cli": "^4.3.0",
    "hexo-deployer-git": "^3.0.0",
    "hexo-generator-archive": "^1.0.0",
    "hexo-generator-baidu-sitemap": "^0.1.9",
    "hexo-generator-category": "^1.0.0",
    "hexo-generator-feed": "^3.0.0",
    "hexo-generator-index": "^2.0.0",
    "hexo-generator-search": "^2.4.1",
    "hexo-generator-sitemap": "^2.1.0",
    "hexo-generator-tag": "^1.0.0",
    "hexo-hide-posts": "^0.1.1",
    "hexo-neat": "^1.0.9",
    "hexo-renderer-ejs": "^1.0.0",
    "hexo-renderer-marked": "^3.0.0",
    "hexo-renderer-pug": "^3.0.0",
    "hexo-renderer-stylus": "^2.0.1",
    "hexo-server": "^2.0.0",
    "hexo-tag-aplayer": "^3.0.4",
    "yamljs": "^0.3.0",
    "hexo-wordcount": "^6.0.1"
```
