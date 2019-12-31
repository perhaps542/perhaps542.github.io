---
title: Note | Disqus记录
date: 2018-05-07 22:38:26
category: Note
tags: technique
---

<center>2018 年的第 1 篇文章</center>

<br>

没想到更新今年的第一篇文章居然是 2018 基本已经过了一半了（啊呸，就凭我的懒惰程度，怎么可能没想到呢...23333

今天主要是花了十来分钟，给博客加了一个 Disqus ————虽然并没有人来评论...既然加了，那就稍微记录一下这个过程吧！

> 关于 Hexo 如何搭建，如何换主题之类的，开博客的时候没有记录，反正 Hexo 有自己的文档，需要的话自己找吧，本文仅从 Blog 已经建好开始。

### 配置 Disqus

首先，请自觉去 [Disqus](https://disqus.com/) 官网注册一个账号，尤其提示一下，如果介意自己的大名暴露在博客里，这里的账号千万不要用带有自己真名的账号（别问我为什么这样提示的）！！！因为最后账号名会大剌剌地躺在这里：

<div style='text-align:center' >
	{% img /Note-Disqus记录/5.jpeg 820 332 图1%}
</div>

<br>

注册好账号之后，点击页面的「GET STARTED」，选择“I want to install Disqus on my site”，就可以开始填写信息啦，看图看图：

<div style='text-align:center' >
	{% img /Note-Disqus记录/1.jpeg 666 686 图2%}
</div>

<br>

「Website Name」填一个自己的 Short name 即可，但是注意**需要独一无二并且填写后不可修改**，然后随意选个类别，再按需选择语言。

接着点击左侧的「Configure Disqus」，填写前面设置的 Website Name 和你的博客地址。

<div style='text-align:center' >
	{% img /Note-Disqus记录/4.jpeg 1005 456 图3%}
</div>

<br>

一切 OK 后，就完成了 Disqus 的基本设置啦～紧接需要配置 Hexo 啦！

### 配置 Hexo

在 Hexo 的一级目录下的_config.yml 添加

```
# Write your shortname
disqus_shortname: 最开始设置的 Website Name
```

然后进入 theme 目录，这里我用的主题是 Huno , Huno 下找到了 duoshuo.ejs ，我就不费劲儿改文件名了（我的是在 blog/themes/Huno/layout/_partial/duoshuo.ejs，不同主题请自行查找，替换为下面的内容

```
<% if (page.comments){ %>
<section id="comment">
  <% if(config.disqus_shortname) { %>
  <div id="disqus_thread">
    <noscript>Please enable JavaScript to view the <a href="//disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
  </div>
  <% } %>
</section>
<% } %>
```
接着，修改 blog/themes/Huno/layout/_partial/footer.ejs（我的是这个名称，不同主题自己看着找吧），将原来的多说相关的代码删掉，增加下面的代码（根据自己的情况改哈）

```
<% if ((page.layout == 'post' || page.layout == 'page') && config.disqus_shortname && page.comments){ %>
    <script type="text/javascript">
    var disqus_shortname = '<%= config.disqus_shortname %>';
    var disqus_config = function () {
        this.page.url = '<%= config.url %>/<%= page.path %>';
        this.page.identifier = '/<%= page.path %>';
        this.page.title = '<%= page.title %>';
    };
    (function(){
      var d = document;
      var dsq = d.createElement('script');
      dsq.type = 'text/javascript';
      dsq.async = true;
      dsq.src = '//' + disqus_shortname + '.disqus.com/<% if (page.comments){ %>embed.js<% } else { %>count.js<% } %>';
      (d.head || d.body).appendChild(dsq);
    })();
    </script>
<% } %>
```

最后开整

```
hexo clean
hexo g
hexo s
```

齐活儿～这玩意儿还是比较容易的，我就是为了凑一篇文章，好了，睡觉！

<br>







