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
swiper_index: 4
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

### vercel
咕咕咕… 继续来写吧，Vercel算是一个不错的托管商，速度是这三个里面最快的，而且它还可以线上托管代码函数api执行，这些先搁着不讲，如何把网站部署到Vercel上呢？
#### 克隆源代码
因为Hexo自带源代码和github page克隆，所以这个方法简单，每次部署到Github上之后就会自动克隆过去并转化成静态页面，相当于部署了动态博客。
#### 注册

Vercel的注册也很简单，进入vercel.com/signup，由于是国外网站，所以进去会很慢，建议搭配Steam++食用。（没恰饭啦）
一般都是用github登录，点Continue with Github，如果你授权过Github的话，会直接进入，没登录就登陆呗。没有授权过的会进入授权界面（图找不到了，网图，侵删），大概如图
点击绿色按钮就能自动登录了（网络不好容易登陆失败）。
如果出现灰色点不了的现象，请检查：
- 是否是用的手机浏览器（夸克、UC等），如果是请使用微信（新版）自带浏览器，实测可以过Github。
- 是否用的浏览器版本过时，请更新。
- 是否用的是IE，Github不支持。

#### 部署
进入仪表板，你会看到这个界面(我这里之前已经有过项目了，应该是空的)（博主居然懒得为了科普开小号，垃圾博主再也不关注了）
点击New Project，从你的Github导入博客对应的Pages仓库
选择你博客Pages的仓库，import即可。
这个配置界面我们并不需要选择什么，只要确认framework-reset为other，修改project name为你想要的名字（不宜太长！！！），点击Deploy即可部署。
部署之后用 项目名.vercel.app进入博客就行了，跟Cloudflare一样，Vercel也会给你颁发有效期为三个月的R3证书并自动续期，每次博客部署到Github也会同步进行。

#### 调整节点
虽然Vercel没有大陆节点，但是还是有香港节点的，还是要调整一下，会加快一点速度。香港节点永远都是最能用的，一国两制yyds
进入项目主页，选择Setting-Serverless Functions，在右侧选择框选择Hong Kong(East)-hkg1
设置节点之后下一次部署就会生效

#### 绑定自己的域名
返回项目主页，选择顶部的Setting-Domains
在顶部的文本框输入你的域名，比如wyblog.eu.org，点击Add，这个选择框是让你选择www和根域名的关系（第一个就是输入根域名跳转到www，第二个就是输入www会跳转到根域名，根据你的喜好选择（如果不是www或者根域名就没有提示）），我选择第二个，然后点击Add就行了。
添加之后它会让你加入A记录或者CNAME记录，按照它的提升添加，Vercel会给你颁发证书，稍等一会即可正常访问了。

### Netlify
Netlify同样也是一家老牌网站托管商，但是国内常被GFW墙掉，所以不是很建议选择。不过不抽的时候也挺快，有些地区速度不错。

#### 注册
Netlify的注册托管也很简单，进入app.netlify.com，选择Github登录
跟Vercel一样，会进入Github的验证界面，按照前面的方式验证。
接下来它会让你填一些信息，这个可以随便填。

#### 部署
接下来部署项目，Netlify注册后会自动进入首次部署界面，选择从Import from Git
选择你的Github源代码对应的仓库
进入部署选项界面，你会看到它在加载分支。
不知道是什么bugBugjump：特性！，它会一直加载分支，这时你需要手动点击“Customize build settings”来加载
加载完后，选项不用改，直接点击Deploy site即可
不同于vercel，Netlify的首次部署较慢，总之等一等就好了。
等到部署完成之后，你就可以用 项目名.netlify.app访问站点了，不同的是，Netlify的项目名是自动生成的，就是顶上导航栏的那一个。

#### 更改项目名
如果你不喜欢这个名字当然也可以更改项目名，进入项目主页-Site settings-General-Site Details，选择右侧的Change Site name，输入自己喜欢的名字，Save即可。
Netlify也会自动给你颁发R3证书并自动续期，同样每一次hexo d会自动部署到Netlify上面。

#### 绑定自己的域名
进入项目主页-Site settings-Domain management-domains
选择Add domain alias，输入你的域名，域名就添加成功了。
如果你没有预先设置cname的话，就选择域名后面的，然后按照上面的方式把域名解析到上面就好了。
开始研究你的网站吧！

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
