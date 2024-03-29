# findhappytime


致谢
====================================

使用
====================================

下载
------------------------------------

使用git从[findhappytime](https://github.com/findhappytime/findhappytime.github.io.git)主页下载项目

```  git bash
git clone https://github.com/findhappytime/findhappytime.github.io.git
```

配置
------------------------------------

`findhappytime`项目需要配置的只有一个文件`_config.yml`，打开之后按照如下进行配置。

> 特别注意`baseurl`的配置。如果是`***.github.io`项目，不修改为空''的话，会导致JS,CSS等静态资源无法找到的错误

``` bash
name: 博客名称
email: 邮箱地址
author: 作者名
url: 个人网站
### baseurl修改为项目名，如果项目是'***.github.io'，则设置为空''
baseurl: "/findhappytime"
resume_site: 个人简历网站
github: github地址
github_username: github用户名称
FB:
  comments :
    provider : duoshuo
    duoshuo:
        short_name : 多说账户
    disqus :
        short_name : Disqus账户
```

如何写文章
------------------------------------

在`LessOrMore/_posts`目录下新建一个文件，可以创建文件夹并在文件夹中添加文件，方便维护。在新建文件中粘贴如下信息，并修改以下的`titile`,`date`,`categories`,`tag`的相关信息，添加`* content {:toc}`为目录相关信息，在进行正文书写前需要在目录和正文之间输入至少2行空行。然后按照正常的Markdown语法书写正文。

``` bash
---
layout: post
#标题配置
title:  标题
#时间配置
date:   2016-08-27 01:08:00 +0800
#大类配置
categories: document
#小类配置
tag: 教程
---

* content
{:toc}


我是正文。我是正文。我是正文。我是正文。我是正文。我是正文。
```

执行
------------------------------------

``` bash
jekyll server
```

效果
------------------------------------
打开浏览器并输入URL`http://localhost:4000/`,回车。


为什么重复造轮子
====================================

很明显，我在重复造轮子。在13年接触到GIT，14年末接触到Jekyll，然后搭建了自己的博客，当时是选用了[JekyllThemes](http://jekyllthemes.org/)上的[Solar](https://github.com/mattvh/solar-theme-jekyll)主题，一直到现在。不过中间一直感觉页面风格还是偏暗，阅读不方便。并且有一些小的细节做的不是很好。在页面的跨平台浏览上有一些瑕疵。并且不区分一级标题和二级标题，导致没有重点强调。诸如此类，用了2年，用的越多，越发吃力，中间就一直在寻找新的能够让我一眼认定的主题。

虽然设计好看的主题很多。但是真正适合拿来做博客的却不多。中间一直没有找到合适的主题。直到有一天看到Less官网的主题之后，豁然觉得这就是我的博客想要的样子。简单而又不平凡。所以就决定了要把博客迁移到这个主题，然后拿了两天晚上来把这个主题做出来。

重复造了轮子，但是这个是迄今为止自己觉得最适合我的博客的轮子，所以是值得的！

关于作者
====================================



关于打赏
====================================

如果你也像我一样在寻觅一个简洁的博客主题。不妨试下findhappytime。

当然你也可以为了我的工作打赏！以激励我做出更好的东西。

支付宝
----------------

<img src="/styles/images/zhifubao.jpg" alt="支付宝二维码付款给" width="310" />

微信
----------------
![微信二维码付款给findhappytime](/styles/images/weixin.png)
