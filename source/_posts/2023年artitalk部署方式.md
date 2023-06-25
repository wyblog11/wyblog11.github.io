---
title: 2023年artitalk部署方式
categories: artitalk
tags: 说说
cover: https://images.boysec.cn/cover1.webp
mathjax: true
katex: true
type: "post"
description: 最新artalk部署方式
abbrlink: 13221
date: 2023-01-26 20:05:10
swiper_index: 3 #置顶轮播图顺序，需填非负整数，数字越大越靠前
top_group_index: 3 #右侧磁帖顺序，需填非负整数，数字越大越靠前
---
artalk部署方式：
1.在leancloud国际版去注册一个应用(没有就注册一个账号)
2.绑定一下自定义域名(可以是自己的分域名,也可以是网上免费的二级域名,这个域名没有太多要求,只要能访问就行)
3.在结构化数据中创建 class,命名为 shuoshuo
4.在你新建的应用中找到结构化数据下的用户.点击添加用户,输入想用的用户名及密码.(注意:权限不能给用户,因为会导致在访问自己的说说时会出现跨域问题)
5.然后新建一个名为atComment的class,权限什么的使用默认的即可.
6.点击 class 下的 user添加列，列名称为 img,默认值填上你这个账号想要用的发布说说的头像url，这一项不进行配置，说说头像会显示为默认头像
7.默认值填上你这个账号想要用的发布说说的头像url,这一项不进行配置，说说头像会显示为默认头像 —— Artitalk 的 logo.
8.在最菜单栏中找到设置-> 应用 keys,记下来 AppID 和 AppKey,在博客引入以下代码:
```<!-- 引用 artitalk -->
<script type="text/javascript" src="https://unpkg.com/artitalk"></script>
<!-- 存放说说的容器 -->
<div id="artitalk_main"></div>
<script>
new Artitalk({
    appId: '', // Your LeanCloud appId
    appKey: '', // Your LeanCloud appKey
    serverURL: ''// 引入自己绑定的leancloud域名
})
</script>
```
