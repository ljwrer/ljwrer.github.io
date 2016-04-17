---
title: '我搭建了 hexo blog!'
date: 2016-04-16 15:13:21
categories: 日记
tags: 
- hexo
- node
- git
- github

---

<div style='margin:0 auto;width:0px;height:0px;overflow:hidden;'>
<img src="/images/avatar.jpeg" width='700'>
</div>

一直以来，都想开通一个blog,一是记录一下工作与生活，二是分享一些自己的idea。先后尝试了qq空间，简书等等，最大的问题就是没有控制权，寄人篱下。自己购买域名和空间，又太麻烦，直到静态blog生成器进入了视野。

去年开始使用github pages的时候看到了官方推荐的Jekyll时就留意了一下，最近趁着项目的测试期，终于有空开始了，于是又搜索了一下blog生成器，发现了更加轻巧的hexo。
<!-- more -->
hexo有哪些好处呢：
- 完全的Markdown支持，编写方便，即时预览
- 众多极简风格的皮肤
- 一键部署
- 搭配github pages完全免费，不用购买域名和服务器了。。。
- 完全的控制权
- Node.js强力驱动，极快的生成速度

尤其是最后一点，对于一枚前端狗来说，今年FEDAY怎么说的：
<img src="/images/ruby.jpg"/>
<img src="/images/js.jpg"/>
能用js解决的问题都用js解决，ruby神马的闪边去。。。

hexo的部署非常简单，只要几条指令，再设置好github pages就OK了。我选择了[next](http://theme-next.iissnan.com "next")主题，极简的风格，而且作者非常勤奋的解决issue，强力推荐。当然部署的过程中也遇到了几个要注意的地方:
 1. 所有的配置文件都要在冒号后接空格，包括yml和markdown内的配置
 2. 你需要的大部分功能，都有现成的插件可以解决，比如资源压缩，安装`hexo-all-minifier`就好了，无需额外的操作，在部署时会自动压缩
 3. 最后就是远程部署的问题,首先参考知乎的问题
{% blockquote CrazyMilk的回答 http://zhihu.com/question/21193762/answer/79109280 使用hexo，如果换了电脑怎么更新博客？ %}
{% endblockquote %}

建立两个分支，需要deploy的内容放到master分支，source内容放到hexo分支然后ignore掉deploy的内容。回到家以后，git clone，发现next主题不见了，原来next也是一个git，提交时会被忽略掉。当然，删掉next下的`.git`就可以提交了，但是我又想保持和线上的更新，怎么办呢，使用fork+submodule+pull request:
## fork
首先将主题的repo fork 到你的github账号下，以hexo为例，这时next的github地址为
``` bash
git@github.com:yourname/hexo-theme-next.git
```
## 添加submodule
{% codeblock path/to/yourname.github.io master %}
$ git submodule add git@github.com:yourname/hexo-theme-next.git themes/next
{% endcodeblock %}
## 更新主题
将作者的repo pull request 到你的账号，然后
{% codeblock path/to/yourname.github.io/themes/next master %}
$ cd path/to/yourname.github.io/themes/next
$ git pull
{% endcodeblock %}
## 提交主题
{% codeblock path/to/yourname.github.io/themes/next master %}
$ cd path/to/yourname.github.io/themes/next
$ git checkout master
$ git add <stuff>
$ git commit -m "comment"
$ git push
{% endcodeblock %}
{% codeblock path/to/yourname.github.io/%}
$ cd path/to/yourname.github.io
$ git add themes/next
$ git commit -m "updated my theme next"
$ git push
{% endcodeblock %}
## 远程部署
{% codeblock bash %}
$ cd path/to/
$ git clone <url>
$ git submodule init
$ git submodule update
$ npm install hexo-cli -g
$ npm install
$ hexo new post <title>
$ hexo g -d
{% endcodeblock %}
总的来说，如下图所示：
<img src="/images/hexo.svg">

好啦，终于有自己的小窝了，接下来要做的事情就是Keep Blogging!



