---
title: 使用replit搭建artalk后端
categories:
  - 教程
  - replit
date: '2023-06-21 17:34:17'
cover: https://cdn-us.imgs.moe/2023/06/05/647de033ccff9.png
tags:
  - replit
  - artalk
  - 折腾
  - 白嫖
swiper_index: 6 #置顶轮播图顺序，需填非负整数，数字越大越靠前
---
#### 1.前往[https://replit.com/](https://replit.com/)注册账号（推荐用github）

#### 2. 依次点击


![https://image.yuanning0818.tk/1687340309986.png](https://image.yuanning0818.tk/1687340309986.png)

#### 3.打开shell，右键粘贴以下命令,回车

```shell
git clone https://github.com/ning0818/artalk-replit 
mv -b artalk-replit/* ./ 
mv -b artalk-replit/.[^.]* ./ 
rm -rf *~ 
rm -rf artalk-replit
```

![https://image.yuanning0818.tk/1687340901678.png](https://image.yuanning0818.tk/1687340901678.png)

#### 4.当shell输出

```shell
Cloning into 'artalk-replit'...
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 9 (delta 1), reused 7 (delta 0), pack-reused 0
Receiving objects: 100% (9/9), 33.33 KiB | 3.33 MiB/s, done.
Resolving deltas: 100% (1/1), done.
Detected change in environment, reloading shell...
```

时，点击上面的run

![https://image.yuanning0818.tk/1687341043638.png](https://image.yuanning0818.tk/1687341043638.png)

#### 5.打开artalk-go.yml，你要修改的：

![https://image.yuanning0818.tk/1687341200609.png](https://image.yuanning0818.tk/1687341200609.png)

注：密码需加密，推荐https://cmd5.com

#### 6.这就是你的后端地址

[artalk](https://artalk-replit.wyblog.repl.co/)

#### 7.参考官方文档
[👋 Hello Friend | Artalk](https://artalk.js.org/guide/intro.html)

#### 8.后记
artalk2.3.0以后基本上没法用replit部署，只能用docker部署。
