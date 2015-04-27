---
layout: post
title: Web Spider
category: python
tags: Python Spider
keywords: Python web Spider
description: mark
---

1 网络爬虫，即Web Spider
2 URL和URI
URL就是在浏览器端输入的    http://www.baidu.com    这个字符串。
什么是URI？
Web上每种可用的资源，如 HTML文档、图像、视频片段、程序等都由一个通用资源标志符(Universal Resource Identifier， URI)进行定位。 
URI通常由三部分组成：
①访问资源的命名机制；
②存放资源的主机名；
③资源自身 的名称，由路径表示。
如下面的URI：
http://www.why.com.cn/myhtml/html1223/
我们可以这样解释它：
①这是一个可以通过HTTP协议访问的资源，
②位于主机 www.webmonkey.com.cn上，
③通过路径“/html/html40”访问。 
URL是URI的一个子集。它是Uniform Resource Locator的缩写，译为“统一资源定位 符”。
通俗地说，URL是Internet上描述信息资源的字符串，主要用在各种WWW客户程序和服务器程序上。
采用URL可以用一种统一的格式来描述各种信息资源，包括文件、服务器的地址和目录等。
URL的一般格式为(带方括号[]的为可选项)：
protocol :// hostname[:port] / path / [;parameters][?query]#fragment

URL的格式由三部分组成： 
①第一部分是协议(或称为服务方式)。
②第二部分是存有该资源的主机IP地址(有时也包括端口号)。
③第三部分是主机资源的具体地址，如目录和文件名等。
第一部分和第二部分用“://”符号隔开，
第二部分和第三部分用“/”符号隔开。
第一部分和第二部分是不可缺少的，第三部分有时可以省略。 

五、URL和URI简单比较
URI属于URL更低层次的抽象，一种字符串文本标准。
换句话说，URI属于父类，而URL属于URI的子类。URL是URI的一个子集。
URI的定义是：统一资源标识符；
URL的定义是：统一资源定位符。
二者的区别在于，URI表示请求服务器的路径，定义这么一个资源。
而URL同时说明要如何访问这个资源（http://）。