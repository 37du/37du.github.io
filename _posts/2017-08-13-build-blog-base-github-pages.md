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
 # Hello World!
 ```
   5. git push 发布你所有的内容到 GitHub 上， 访问 https://username.github.io, 就可以看到 Hello World! 以 Hacker 那种样式展示了。
   >  这种快速使用模版的方式， 其实就只选择一下主题， 然后就可以写Markdown文档， 那么问题来了， 如果我有很多文档， 如何对文档进行导航呢， 还有如何分类呢， 我还显示个人信息呢, 站内搜索呢。 很可惜， 目前官方提供的快捷主题使用， 不支持那么多特性， 需要用户自己去定制这些特性, 下面会说到一些解决方案。

* Project Pages
   与上面的类似， 只是访问时， 是使用 https://username.github.io/projectname, 另外还有分支上的区别， 详见[官网](https://help.github.com/articles/user-organization-and-project-pages/)

GitHub 提供快速使用模块， 只需要选择主题即可， 缺点是提供的特性非常有限. 如果添加[GitHub 支持的 Theme](https://pages.github.com/themes/), 就只需修改 _config.yml， 在 _config.yml 中指明使用什么 Theme. 后面会谈到解决方案。

#### GitHub Pages 支持的 Jekyll Theme

GitHub Pages 支持的 Jekyll Theme , 可以在不需要编辑或复制主题模版的文件情况以不同的设计样式展示你的博客。 其实这些主题模版的文件都被打包到 assets 目录里， assets 目录在本地是在 _site 目录里， 后面会有介绍。 并不是所有 Jekyll Theme 都被 GitHub Pages 支持， Github Pages 支持的 Jekyll Theme 就是前面说到的快速使用的模版。

GitHub Pages 支持的 Jekyll Theme 的目录结构：
 * _layouts
 * _includes
 * _sass
 * assets
 如果想重新配置或者修改某些配置或样式， 需要阅读你选择的 Theme 的 README 或其他文档。

#### 本地 Preview 主题

首先需要按装[Bundler](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/#requirements), 以下是安装步骤:

1. 打开命令行， 检查一下本地是否有 Ruby 2.1.0 或以上， 如果没有， [安装 Ruby 2.1.0 或以上](https://www.ruby-lang.org/en/downloads/)
> 这里要注意下， macOs 上自带 Ruby ， 但是版本是 1.8.x ， 版本比较低， 如果不是 2.1.0 或以上版本， 之后安装 Bundler 时， 会有很多问题。所以一定要确保 Ruby 版本是 2.1.0 或以上。

2. 安装 Bundler,  在命令行执行  gem install bundler
>  如果在安装 Bundler 出现其他问题， 请自行 Google

这里使用上面写的 Hello World 的 GitHub Pages site ， 打开命令行进入到本地 repository 目录，先 git pull 同步 remote 最新的内容， 然后新建 Gemfile 文件， 添加如下两行内容：
```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

随后执行 bundle install, 就可以安装 Jekyll theme 了， 然后执行 bundle exec jekyll serve， 本地浏览器访问 localhost:4000 就可以看见博客主页， 这时在本地就可以看到上面之前讲到访问 https://username.github.io 一样的效果， 效果如下：
![Alt text](/images/2017-08-13-build-1.1.png)

讲到这里， 无论是使用主题， 或本地 preview 主题效果， 操作都非常简单， 你甚至都不知道 Jekyll Theme 的静态网页有哪些文件， 你所知道只有 _config.yml, Gemfile 以及你想要写的 md 文件，那么 Jekyll Theme 的静态网页文件在哪里呢， 本地的话， 在运行 bundle exec jekyll serve 就会在本地产生 _site 目录， 这里会看见有 index.html (静态网页) 和 assets (资源文件, 里面可能有 css, fonts, js等子目录), 也就是上面提到的 GitHub Pages 支持的 Jekyll Theme 会把这些文件都打包到 assets 目录里。

#### [自定义 Theme](https://help.github.com/articles/customizing-css-and-html-in-your-jekyll-theme/)

GitHub Pages 支持的 Jekyll Theme 会通过提供 README 文件说明如何自定义你的主题， 例如前面选择了 Hacker Theme, 那么 [Hacker 提供的 README](https://github.com/pages-themes/hacker#customizing) 会说明如何自定义你的 Hacker 主题。

##### 自定义主题样式
1. 在本地 repository 目录下， 新建目录 /assets/css ， 然后在 ／assets/css 目录下新建 style.scss 文件， 添加如下内容:

```
 ---
 ---

 @import "{{ site.theme }}";
```

2. 在上面添加的 @import 那一行的下面添加任意你喜欢的自定义CSS样式内容， 例如想把大标题的字体颜色改成灰色：

```
 ---
 ---

 @import "{{ site.theme }}";

 h1 {
    color: #888;
 }
```

访问 http://localhost:4000 你会看到如下效果(对比图-1.1)：
![Alt text](/images/2017-08-13-build-1.2.png)

### 自定义布局

1. 先找到你选择的主题的源 GitHub repository 中 _layout 目录下的 default.html 文件, 例如上面选择 Harker 主题， 那么 defualt.html 文件就通过 https://github.com/pages-themes/Harker/blob/master/_layout/defualt.html 找到了。
2. 复制上一步中的 default.html 文件内容， 并在你本地的 repository 中也要新增目录 _layout 并在其下新增文件 default.html, 内容为刚才复制的内容。
3. 在本地 repository 中的 _layout 下的 defualt.html 文件， 你可以添加任何静态网页的内容来定制你的布局。

这里就不举例了， 类似上面自定义主题样式。

### Jekyll Theme 的工作原理

通过上述内容， 我们可以在完全不知道有静态网页的情况完成主题的配置及使用， 那么这是如何工作的呢， 其实在 _site 下就包含了静态网页的相关文件， 只是这些都本地 Jekyll 自动生成， 我们完全不用关心。

工作原理可以参考[利用github-pages建立个人博客](https://www.ezlippi.com/blog/2015/03/github-pages-blog.html) 中的第7小节的介绍。

可以下载[jekyll原作者推荐的例子](https://github.com/plusjade/jekyll-bootstrap)来学习一下。

### 直接使用你觉得不错的博客的主题

现在已经知道 Jekyll Theme 包含了什么文件了， 那么就可以直接使用别人的博客主题了(删除主题无关的文件， 只复制主题相关的文件来覆盖本地 repository 的主题相关文件)，可以分以下几步：
1. 可以通过 [jekyll wiki site](https://github.com/jekyll/jekyll/wiki/sites) 和 [GitHub Pages examples](https://github.com/showcases/github-pages-examples) 找自己满意的博客主题， 例如我找到[码志](http://mazhuang.org/)，然后找到对应的 [GitHub Pages repository](https://github.com/mzlogin/mzlogin.github.io), 这个博客包含搜索、分类、评论等特性， 然后把别人的博客repository Clone 到本地。
2. 进入到 Clone 下来的本地目录， 删除 _posts(保存发布的 md 文件), _drafts(作为草稿的 md 文件), _wiki(可能你选择的主题没有这个目录， 这个目录是上面码志的博客特有的目录), images(存放图片, 这个目录也是博客自定义目录), 这几个目录的特点就是存放博客内 Markdown 文件相关的资源， 例如 md文件， 以及 md 文件用到的图片文件， 所以基本上涉及到博客发表的文章相关内容都删除。
3. 复制剩余的目录或文件到你本地自己博客 repository ， 然后查看源主题的 README 是否有说明如何修改成自己全局配置， 即修改 _config.yml 。
4. 使用码志这个例子， 来修改 _config.yml, README 中有说明, 以下内容只是贴出部分修改结果, 是个例子， 完整的可以参考[我的博客 _config.yml](https://github.com/37du/37du.github.io/blob/master/_config.yml)：

```
  # 注意这里的 username 都是自己的 GitHub 用户名

  baseurl:
  url: http://usename.github.io
  title: 自己的博客标题
  subtitle:  博客标题的副标题

  author: username

  gitment:   
      owenr: username
      repo:  usename.github.io
      oauth:
          client_id:  自己申请的client_id
          client_secret:  自己申请的 client_secret

  # google:    别人注册的统计id, 就不要使用了
  #       analytics_id: ******
```

5. 然后就是在本地访问 localhost:4000 来看下修改后的结果了， 可能有些需要调整的， 例如源博客有其他 Pages 的内容不支持 _config.yml 配置， 关于这部分内容需要自己来调整， 例如上面的码志的博客“链接”那个页面里面的链接地址都是在 _data 目录配置的， 如果你想换成自己的链接地址， 就需要修改 _data 下的文件了。
6. 在本地调整完了， 就可以 git push 到 GitHub 上了。

这里简单介绍主下题模版的目录结构， 即Kekyll Theme. 通过上面的 Jekyll Theme Chooser 可以看到一些开源的主题的源码， 可以观察到他们的 repository 的目录结构， 这里就引入了 [Jekyll 目录结构](https://jekyllrb.com/docs/structure/)的概念了， 简单的说就是以下几点：
1. index.html  博客主页, 这个页面是主题提供， 访问你的博客，就看到这个页面， 一般用于展示所有的博客引索。
2. _config.yml  全局配置文件， 这个文件主题模版会提供一些配置， 按需修改里面的配置， 例如全局的 url 可以改成自己的博客网站url
3. layouts      静态网页模版， 例如博客分类页面， wiki 页面，详细个人信息页面等, 一般都是 html 文件。
4. include     部分静态网页模版， 可以被 layouts 里面的模版混合引用， 例如 页眉和页脚， 评论等静态网页的子布局， 这些都是可以被重复使用的。
5. assets      资源目录， 可以包含一些子目录， 例如 css 存放静态网页的 css 文件， js 存放 javascript 文件， image 存放图片资源。
  >   这里跟官网上给的目录结构有点不一样， 官网没有提到 assets, 其实就是官网提到的 Other Files/Folders,  例如上面码志的博客 image 目录就是 Other Folders 类型。

## [自定义域名](https://help.github.com/articles/using-a-custom-domain-with-github-pages/)

GitHub Pages 支持配置自定义域名， 例如我要通过 https://37du.github.io 访问自己的博客， 配置来自定域名(完整的域名是 www.eai37.com), 那么配置自定义域名后，就可以通过 http://eai37.com 或 http://www.eai37.com 来博客了。

首先要购买个域名， 国内有很多域名提供商， 我是在Godaddy上购买的域名(www.eai37.com)。 看下支持的自定义域名类型， www.eai37.com 是 www 子域名类型， 那么 eai37.com 就是主域名， www 是主机的意思。

然后在[添加自定义域名到你的 GitHub Pages site](https://help.github.com/articles/adding-or-removing-a-custom-domain-for-your-github-pages-site/), 例如你的域名是 www.eai37.com 那么在 "Setting -> Custom domian" 处填写你的主域名即可， 填写 eai37.com。

最后就是设置你的 DNS 提供商如何解析你的购买的域名了， 例如选择国内的 DNS 提供商 [DNSPOD](https://www.dnspod.cn/), 注册账号， 然后在安装下图操作即可。
![Alt text](/images/2017-08-13-build-1.3.jpeg)
![Alt text](/images/2017-08-13-build-1.4.jpeg)

配置完你选择的 DNS 提供商后， 要把你购买域名的提供商的域名服务器指向你选择的 DNS 提供商， 如下图配置：
![Alt text](/images/2017-08-13-build-1.5.jpeg)

要验证自己是否有配置正确， 可以在命令行运行如下命令 ：
![Alt text](/images/2017-08-13-build-1.6.jpeg)

解释一下， CNAME 是别名的意思， 即访问 http://www.eai37.com ，访问 http://eai37.com ， 与访问 https://37du.github.io 三种访问方式结果一样.


# 参考
[如何搭建一个独立博客——简明 GitHub Pages与 jekyll 教程](http://www.cnfeat.com/blog/2014/05/10/how-to-build-a-blog/) <br/>
[利用github-pages建立个人博客](https://www.ezlippi.com/blog/2015/03/github-pages-blog.html) <br/>
[搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
