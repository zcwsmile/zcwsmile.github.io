---
layout: post
title: 使用Jekyll和Github搭建博客
category: 技术
tags: Jekyll
keywords: jekyll,github,markdown,ruby 
---

>假设你熟悉git,懂得一点ruby环境配置，熟悉linux的基本命令，热衷于markdown标记语言来编写文本，那么不妨选择Jekyll来搭建静态博客。接下来我将一步步地描述本博客的搭建步骤。

###Jekyll环境搭建
1.安装ruby。

    $ sudo apt-get install ruby1.9.1-dev
2.设置ruby的源。

	$ gem sources --remove http://rubygems.org/
    $ gem sources -a http://ruby.taobao.org/
3.ubuntu下需要自己安装nodejs, 等一些其他的包。(如果没安装下面的包，运行jekyll server命令会遇到ExecJS::RuntimeUnavailable错误)

	$ sudo apt-get install python-software-properties
	$ sudo add-apt-repository ppa:chris-lea/node.js
	$ sudo apt-get update
	$ sudo apt-get install nodejs
4.安装Jekyll。

	$ sudo gem install jekyll
5.如果上一步安装过程中没有安装rdoc, rdiscount, kramdown等，可以执行下面步骤安装。

    $ sudo gem install kramdown
	$ sudo gem install rdoc
	$ sudo gem install rdiscount
6.上面步骤执行完后，新建博客目录。

    $ jekyll new myblog
7.运行下面的命令启动。
	
    $ jekyll server
			
###创建主题
在[http://jekyllthemes.org/](http://jekyllthemes.org/)上下载自己喜欢的主题即可，然后启动server即可在本地预览主题效果。

在自己的github上新建一个仓库，命名为`username.github.io`,然后执行以下命令
将本地代码push到远程仓库。如果你是以ssh的方式提交，首先要在github的设置中
添加ssh key。

    touch README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin git@github.com:yuandong618/yuandong618.github.io.git
    git push -u origin master

在浏览器中输入`username.github.io`即可访问自己的博客网站。
###绑定域名
如果你不喜欢通过`username.github.io`来访问自己的网站，可以自己购买域名来访问。我个人推荐在[name](http://www.name.com/)或[godaddy](http://www.godaddy.com/z)这两个国外域名注册商购买域名，我的域名是在[name](http://www.name.com/)上
购买的。

在自己的网站目录下新建一个`CNAME`文件，并将自己的域名写在这个文件里，像我
一样

    yuandong.im

输入以下命令，获取github给我们分配的ip地址。然后在自己的域名管理中添加一条A
记录，记录值为获取到的ip地址，然后在浏览器中输入自己的域名即可访问网站。

    dig yuandong618.github.io  +nostats +nocomments +nocmd
###代码高亮

###博客评论

###谷歌分析(GA)



