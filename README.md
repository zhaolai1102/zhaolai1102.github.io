## 前言

这个博客是使用github pages和jekyll框架搭建的

  - `_config.yml` 全局配置文件
  - `_posts` 放置博客文章的文件夹
  - `img` 存放图片的文件夹  
  - `CHANE` 博客的域名

#### `_config.yml` 配置文件

> Site settings基础设置

```
# Site settings
title: Fe Blog  #你博客的标题
SEOTitle: Fe的博客 | Fe Blog  #显示在浏览器上搜索的时候显示的标题
header-img: img/404-bg.jpg #显示在首页的背景图片
email: fedemo@foxmail.com
description: "Every failure is leading towards success." #网站介绍
keyword: "Fe, Fe Blog, Fe的博客,JAVA" #关键词
url: "http://fedemo.top"          # your host, for absolute URL
baseurl: ""      # for example, '/blog' if your blog hosted on 'host/blog'
github_repo: "https://github.com/FeDemo/fedemo.github.io.git" # you code repository
```
<br>
> Sidebar settings侧边栏设置

```
# Sidebar settings侧边栏
sidebar: true                           # 是否开启侧边栏
sidebar-about-description: "Goals determine what you going to be!" #装B的话
sidebar-avatar: /img/avatar_m.jpg      # 你的头像
```
<br>
>  SNS settings社交账号

```
# SNS settings社交账号  如果没有的话注释掉就好了
RSS: false
# weibo_username:
zhihu_username:    fedemo
github_username:    FeDemo
# facebook_username:
jianshu_username:   57064928f3a8
#twitter_username:   fede绑定域名
现在,我们的博客已经可以说是搭好了,你可以把你的网址告诉给你的小伙伴了  

现在,我们的网址是 fedemo.github.io,是属于github下的子域名.  

对于小伙伴来说可能不是那么好记,那么我们现在应该怎么办了?

购买域名
买买买

当然是充钱啊  
￼  

我的话是在百度云买的域名,我的fedemo.top首年只要一块钱

￼

具体购买流程就不细说了  
ps:如果对域名这块不是很熟的可以尝试下阿里云,客户小哥贼热情.  
我当时就用我的淘宝号登上阿里云的网址几次,阿里的客户小哥就打电话过来问我是不是要买服务器.....

解析到我们的博客
DNS解析

这里我以百度云为例,在购买域名后.通过域名服务 / 域名管理 / 域名解析进入域名解析绑定我们的网站

￼

添加解析

￼

主机记录  

主机记录即域名前缀，常用如下：

￼
1. www：解析后域名为 www.fedemo.top
2. @：直接解析主域名 fedemo.top
3. *：泛解析，匹配其他所有域名 *.fedemo.top
一般的话我们只要解析 www 和 @ 就可以了

A记录和CHAME记录的区别  

这里,说明下A记录和CHAME记录的区别  

A记录表示解析到IP地址,所以我们要天地的记录值是ipv4格式的(PS:github的IP地址是 151.101.229.147 )

CHAME记录可以理解为重定向,就是从该域名(fedemo.top)跳转到另外一个域名(fedemo.github.io)

这里,我更推荐使用CHAME记录,因为github的IP地址可能会不稳定,如果github修改的话我们这边也需要修改才可以使用

项目本地CHAME配置

当然,当初地从域名这里解析到github pages还不行,因为这样只是指向了github的ip而已.  
我们还需要告诉github,我这边用你的服务器建了个博客,现在我要绑定域名了

接着,我们需要修改项目根目录下的CHAME文件,打开CHAME,在里面写上你注册的域名(不需要写前缀,只要写fedemo.top就好了)

来,上车
再稍微等一下,我们就可以通过我们购买的域名访问我们的页面了.这篇教程也差不多完了,有不懂得或者踩到什么坑以及有什么意见都可以在下面的评论中说出来

一些补充
域名实名认证

在国内购买的域名都需要实名认证,不然可能给你用几天就给你停掉了

此坑已踩 OTZ

关于文章

我在博客中的文章，你们可以保留，让更多需要帮助人的看到，当然也可以删除。  

不过,保留的话希望能够注明出处,并标明转载,谢谢

Star
如果觉得这篇教程还有点用，请点播关注，给我的github仓库 点个 star 吧！

mo
```
<br>
> Gitalk评论系统

集成了Gitalk评论,这是一个github内的开源项目.基于 Github Issue 和 Preact 开发的评论插件.   
github地址: <a href="https://github.com/gitalk/gitalk" target="view_window">https://github.com/gitalk/gitalk</a>  
需要 Github Application，如果没有 <a href="https://github.com/settings/applications/new" target="view_window">点击这里申请</a>
更加详细的介绍可以看下官方的 <a href="https://github.com/gitalk/gitalk/blob/master/readme-cn.md" target="view_window">中文文档</a>
和这篇<a href="http://qiubaiying.top/2017/12/19/%E4%B8%BA%E5%8D%9A%E5%AE%A2%E6%B7%BB%E5%8A%A0-Gitalk-%E8%AF%84%E8%AE%BA%E6%8F%92%E4%BB%B6/" target="view_window">文章</a>

![](https://raw.githubusercontent.com/FeDemo/img_gitalk/master/2017-12-08-blog_re0/19.png)

注册之后会生成**clientID**和**clientSecret**,将其填入下面的配置文件就可以了  

```
# 评论系统
# Gitalk 如果不需要注释掉或者删了就好了
gitalk:
  enable: true    #是否开启Gitalk评论
  clientID: '75ef4c0ecfb2cd85a8f0'    #生成的clientID 不要用我的
  clientSecret: 'b51aa6b7351f3b3b7a0940714af8489fddb5f905'   #生成的clientSecret 不要用我的
  repo: Blog_Gitalk    #仓库(存放评论的项目)名称
  owner: FeDemo    #github用户名
  admin: FeDemo    #拥有admin权限的用户
```
<br>
> 网站统计

集成了<a href="https://tongji.baidu.com/web/welcome/login" target="view_window">Baidu Analytics</a> 和 <a href="http://www.google.cn/analytics/" target="view_window">Google Analytics</a>，到各个网站注册拿到track_id替换下面的就可以了.   
不要用我的`ba_track_id`!
```
# Analytics settings
# Baidu Analytics
ba_track_id: ef224c004e9c327ca58d50ed4501cb99  #统计账号id(不要用我的`ba_track_id`!)

# Google Analytics
# ga_track_id: 'UA-90855596-1'            # Format: UA-xxxxxx-xx
# ga_domain: auto
```
我用的是百度的统计网站,大概是这样  
![](https://raw.githubusercontent.com/FeDemo/img_gitalk/master/2017-12-08-blog_re0/14.png)    

如果觉得不需要的话,注释掉就好了.最后重要的事说3遍,**不要用我的ba_track_id!**
<br>

>  Featured Tags标签设置

```
# Featured Tags
featured-tags: true                     # 是否使用首页标签
featured-condition-size: 1              # 相同标签数量大于这个数，才会出现在首页
```
这个就是设置标签的,上图  
![](https://raw.githubusercontent.com/FeDemo/img_gitalk/master/2017-12-08-blog_re0/18.png)   
如果是刚开始建站,没有几篇文章的话讲标签数改为0就好了  

<br>
> search搜索插件  

本搜索插件来自<a href="https://github.com/androiddevelop/jekyll-search" target="view_window">小胖轩</a>,效果见右下角或者连续按两下`ctrl`    
具体细节可以看下他的<a href="https://github.com/androiddevelop/jekyll-search" target="view_window">项目</a>
```
#如果不需要可以注释掉
#search plugins
search: true                            # 是否使用搜索插件
```
<br>
> Friends好友链接

```
friends: [
    {
        title: "baidu",
        href: "http://www.baidu.com"
    },{
        title: "BY Blog",
        href: "http://qiubaiying.top/"
    }
]
```
#### `_posts`博客的书写

文件的格式是 `.md` 的 <a href="http://sspai.com/25137/" target="view_window">MarkDown</a> 文件。

我们的博客文章格式采用是 **MarkDown**+ **YAML** 的方式。

<a href="http://www.ruanyifeng.com/blog/2016/07/yaml.html?f=tt" target="view_window">YAML</a> 就是我们配置 `_config`文件用的语言。

<a href="http://sspai.com/25137/" target="view_window">MarkDown</a> 是一种轻量级的「标记语言」，很简单。<a href="http://sspai.com/25137/" target="view_window">花半个小时看一下</a>就能熟练使用了

这是页头的格式
  ```
  ---
  layout:     post                  #不要管他
  title:      从零开始的博客生涯     #标题
  subtitle:   blog_re0              #别名,简介,标题下面的那一行字
  date:       2017-12-08            #发表时间
  author:     Fe                    #作者
  header-img: img/post-bg-rwd.jpg   #背景图片
  catalog: true                     #导航目录,不要管他
  original: true                    #是否原创申明
  tags:                             #标签,可以有多个
      - Blog
      - demo
  ---
  ```