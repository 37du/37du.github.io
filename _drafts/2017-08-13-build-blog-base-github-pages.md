---
layout: post
title: 一步一步搭建基于GitHub Pages的博客
categories: tools, blog, GitHub Pages
description: 一步一步搭建基于GitHub Pages的博客
keywords: blog, GitHub Pages, tools, writing
---

一步一步对着GitHub Pages官方教程搭建blog, 支持自定义域名， 支持 gitment 评论插件.

## GitHub Pages 简单介绍

看下[官网](https://pages.github.com/)上的介绍, 简单总结以下几点：
1.  全部内容都托管在GitHub repository上。
2.  实时编辑， 实时发布内容更改。
3.  分两种：针对个人和组织的， 只能有一个;  每个项目对应一个; 详细区别说明见[官网](https://help.github.com/articles/user-organization-and-project-pages/)

一个简单的搭建过程， 可以一步一步参考官网的流程：
1. Create a repository
2. Clone the repositiory
3. 进入本地 Clone 的项目目录. 编辑个 index.html 文件， 然后 git push 发布。
4. 访问 https://username.github.io 就可以看到刚刚 index.html 呈现的内容了。

至此， 一个 GitHub Pages 网站就搭建好了， 特别简单。

## 如何写博客

看了上面的介绍， 可能会想， 难道我们要写静态网页html作为博客内容， 这样太复杂和麻烦了， 下面将介绍如何配置你的网站， 让你专注于写博客， 即只想写写Markdown格式的文本。

### 配置模版主题

在[官网](https://pages.github.com/)最下面， 看到[Blogging with Jekyll](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/)的教程, 讲解了如何配置你的网站。

[Jekyll](https://jekyllrb.com/)的作用就是把普通文本转变成静态网页和博客， 也就是把Markdown的文件转变成html文件， 例如转变成上面的index.html文件。

根据[Blogging with Jekyll](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/), 我们看一步一步深入。

#### 快速使用模版

使用  Jekyll Theme Chooser ,  User, Organization 和 Project Pages 都可以使用 Theme Chooser.
* User, Organization
   1. 创建一个全新的 User, Organization Pages. 也就是说 username.github.io 这个 repository 下除了 .git 没有任何文件。
   2. 进入“Setting" 下， 找到 GitHub Pages 中的 Theme Chooser,  点击 Change theme, 然后你就可以选择一些主题模版了， 例如你选择了主题 Hacker , 确定选择 Hacker 后， 在 "Commits" 提交记录中看到新增了一条commit(Set theme jekyll-theme-hacker) ， 查看 commit 可以发现在根目录新增文件_config.yml, 内容为： theme: jekyll-theme-hacker ,  其实就是设置了主题。
   3. 我进入到[Hacker](https://github.com/pages-themes/hacker) GitHub 主页， 看到 Usage 的描述， 可以看到第一步的操作上面已经帮我们做了， 而第二步是可选的， 先不执行第二步。
   4. 主题设置完毕， 这时我们可以写博客了， 先要写个 index.md, 如下内容：

 ```
 ---
 layout: default
 ---

 Hello World!
 ```
   5. git push 发布你所有的内容到 GitHub 上， 访问 https://username.github.io, 就可以看到 Hello World! 以 Hacker 那种样式展示了。
   >  这种快速使用模版的方式， 其实就只选择一下主题， 然后就可以写Markdown文档， 那么问题来了， 如果我有很多文档， 如何对文档进行导航呢， 还有如何分类呢， 我还显示个人信息呢, 站内搜索呢。 很可惜， 目前官方提供的快捷主题使用， 不支持那么多特性， 需要用户自己去定制这些特性, 下面会说到一些解决方案。

* Project Pages
   与上面的类似， 只是访问时， 是使用 https://username.github.io/projectname, 另外还有分支上的区别， 详见[官网](https://help.github.com/articles/user-organization-and-project-pages/)

GitHub 提供快速使用模块， 只需要选择主题即可， 缺点是提供的特性非常有限. 如果添加[GitHub 支持的 Theme](https://pages.github.com/themes/), 就只需修改 _config.yml， 在 _config.yml 中指明使用什么 Theme. 后面会谈到解决方案。

#### 本地实时PreView

###### 前提条件
[官网介绍](https://help.github.com/articles/adding-a-jekyll-theme-to-your-github-pages-site/),  开始前确保两件事：
1. 本地 git clone 下来 GitHub Pages site repository, 本地 repository 应该包含主题模版的一些文件，如果按照上述流程操作， 是没有这些文件的， 可以 fork 别人的 repository 作为主题模版。

2. 安装 [Bundler](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/#requirements)

针对上述第一点提到的文件有哪些， 是什么， 就再次详细点介绍主题模版， 即Kekyll Theme. 通过上面的 Jekyll Theme Chooser 可以看到一些开源的主题的源码， 可以观察到他们的 repository 的目录结构， 这里就引入了 [Jekyll 目录结构](https://jekyllrb.com/docs/structure/)的概念了， 简单的说就是以下几点：
1. index.html  博客主页, 这个页面是主题提供， 访问你的博客，就看到这个页面， 一般用于展示所有的博客引索。
2. _config.yml  全局配置文件， 这个文件主题模版会提供一些配置， 按需修改里面的配置， 例如全局的 url 可以改成自己的博客网站url
3. layouts      静态网页模版， 例如博客分类页面， wiki 页面，详细个人信息页面等, 一般都是 html 文件。
4. include     部分静态网页模版， 可以被 layouts 里面的模版混合引用， 例如 页眉和页脚， 评论等静态网页的子布局， 这些都是可以被重复使用的。
5. assets      资源目录， 可以包含一些子目录， 例如 css 存放静态网页的 css 文件， js 存放 javascript 文件， image 存放图片资源。
  >   这里跟官网上给的目录结构有点不一样， 官网没有提到 assets, 其实就是官网提到的 Other Files/Folders。

对于普通只想专注于写作的， 不想捣鼓这些设计网页的用户来说， 可以通过 [jekyll wiki sitehttps://github.com/jekyll/jekyll/wiki/sites) 和 [GitHub Pages examples](https://github.com/showcases/github-pages-examples) 来找到自己喜欢的主题， 例如主题要提供评论， 搜索等特性。找到自己喜欢的主题后， 就可以下载到本地，

##### 安装 [Bundler](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/#requirements) 并使用

1. 打开命令行， 检查一下本地是否有 Ruby 2.1.0 或以上， 如果没有， [安装 Ruby 2.1.0 或以上](https://www.ruby-lang.org/en/downloads/)
> 这里要注意下， macOs 上自带 Ruby ， 但是版本是 1.8.x ， 版本比较低， 如果不是 2.1.0 或以上版本， 之后安装 Bundler 时， 会有很多问题。所以一定要确保 Ruby 版本是 2.1.0 或以上。

2. 安装 Bundler,  在命令行执行  gem install bundler
>  如果在安装 Bundler 出现其他问题， 请自行 Google

3. 进入本地博客 repository 目录， 在 Gemfile 文件中添加如下内容：
```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

4.



#### 找个好的模版来使用
