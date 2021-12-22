---
title: "利用hugo和GitHub Pages搭建一个易用的个人博客"
date: 2021-11-24T16:00:30+08:00
draft: false
tags : [
    "Hugo",
    "GitHub Pages"
]
---

&emsp;&emsp;之前有断断续续在CSDN等平台上写过一些文章，整体上还是比较方便的但是利用平台的缺点包括但不限于

- 文章页面上可能带有广告，降低了页面整体的清洁度和观感
- 页面编辑的自由度低，没法DIY一些有意思的东西
- 迁移性差

&emsp;&emsp;但是如果只是为了搭一个简单的博客去租云服务器的话又感觉不划算，那不如试试利用GitHub Pages免费托管静态页面来搭建一个简单的博客。GitHub Pages的使用非常友好，只需要像平常一样创建一个repository，唯一的要求是这个仓库需要命名为username.github.io（username对应你的github用户名或者组织名）。然后就可以在仓库的Setting--Pages下管理你的GitHub Pages，接下来将网页所需要的css、js、html等资源上传到这个仓库即可。

> 官方快速开始教程 https://pages.github.com/

当然这项免费的服务也有一定的限制
- Published GitHub Pages sites may be no larger than 1 GB.

- GitHub Pages sites have a soft bandwidth limit of 100GB per month.

- GitHub Pages sites have a soft limit of 10 builds per hour.

  

  项目大小最大为1GB，每月带宽使用不超过100GB，每小时最多构建10个版本。这个限制对于普通的个人博客而言已经绰绰有余了，可以放心使用


![mypage](../../images/mypage.png)

> 上图为本博客的GitHub Pages供参考，项目地址 https://github.com/thmiao/thmiao.github.io



&emsp;&emsp;有了页面托管的地址就可以开始着手做静态页面了，比起从头开始，选择静态页面的生成框架会更加方便。主流的生成器有jekyll、hugo、hexo、gatsby等。在下作为一个gopher，选用的是golang编写的开源框架hugo作为本站的生成器。

> hugo官网 https://gohugo.io/
>
> hugo项目 https://github.com/gohugoio/hugo

&emsp;&emsp;hugo的安装和使用在hugo官网的quick start已经介绍的非常清楚并且配了动图，本文就不再做赘述和搬运了。利用hugo生成对应的静态页面后，去github仓库的sSetting--Pages下将Sources设置为指定分支的对应根目录，然后push上去就ok了。