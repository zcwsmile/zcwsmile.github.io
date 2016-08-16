---
layout: post
title: CocoaPods安装和使用
category: iOS
tags: iOS CocoaPods Pods
keywords: CocoaPods Pods ios
description: CocoaPods
---


目录
CocoaPods是什么？
如何下载和安装CocoaPods？
如何使用CocoaPods？
查找第三方库


## 1、CocoaPods是什么？
CocoaPods Wiki(https://github.com/CocoaPods/CocoaPods/wiki)
CocoaPods是iOS最常用最有名的类库管理工具了，它能自动将这些第三方开源库的源码下载下来，并且为我的工程设置好相应的系统依赖和编译参数。

## 2、如何下载和安装CocoaPods？
使用mac自带的ruby即可下载安装，很简单，请google一下，本文不再涉及。
在Terminator（也就是终端）中输入以下命令（注意，本文所有命令都是在终端中输入并运行的。
$ sudo gem install cocoapods
$ pod setup

但是，如果你在天朝，在终端中敲入这个命令之后，会发现半天没有任何反应。原因无他，因为那堵墙阻挡了cocoapods.org。
我们可以用淘宝的Ruby镜像来访问cocoapods。按照下面的顺序在终端中敲入依次敲入命令：
$ gem sources --remove https://rubygems.org/
$ gem sources -a https://ruby.taobao.org/        //已经升级成https了
$ gem sources -l                                //验证你的Ruby镜像是并且仅是https://ruby.taobao.org/

1、这时候，你再次在终端中运行：
$ sudo gem install cocoapods
等上十几秒钟，CocoaPods就可以在你本地下载并且安装好了，不再需要其他设置。
2、$ pod setup   //发现不动了,就是慢啊,将这些Podspec索引文件更新到本地的~/.cocoapods/目录下。

(还没明白这个意思：不先pod setup 下面这命令打不了)
使用CocoaPods的镜像索引，如下操作可以将CocoaPods设置成使用akinliu建立的国内服务器镜像，gitcafe（https://gitcafe.com/）和oschina(https://www.oschina.net/)
$ pod repo remove master
$ pod repo add master https://gitcafe.com/akuandev/Specs.git   //可换成oschina的地址
$ pod repo update

## 3、如何使用CocoaPods？

1、在项目根目录下新建一个名为Podfile的文件，将依赖的库写入文件即可：
platform: ios
pod 'JSONKit', '~> 1.4'
pod 'Reachability', '~> 3.0.0'

然后在该项目根目录下执行命令：
$ pod install
所有列出的第三方库都已经下载好并设置好
然后使用CocoaPods 生成的*.xcworkspace 文件来打开工程。
每次更改完Podfile,都需要重新执行一次pod update命令。

platform :ios, '7.0'
pod "AFNetworking", "~> 2.0"
注意：这两句文字的意思是，当前AFNetworking支持的iOS最高版本是iOS 7.0, 要下载的AFNetworking版本是2.0。
$ pod install只会按照Podfile的要求来请求类库，如果类库版本号有变化，那么将获取失败。但是 $ pod update会更新所有的类库，获取最新版本的类库。而且你会发现，如果用了 $ pod update，再用 $ pod install 就成功了。
那你每次直接用 $ pod update 算了。或者先用 $ pod install，如果不行，再用 $ pod update。
不要把Podfile.lock加入到.gitignore中，为保持团队协作第三方库版本一致。

## 4、查找第三方库
利用CocoaPods，在项目中导入AFNetworking类库
AFNetworking类库在GitHub地址是：https://github.com/AFNetworking/AFNetworking
为了确定AFNetworking是否支持CocoaPods，可以用CocoaPods的搜索功能验证一下。在终端中输入：

$ pod search AFNetworking
过几秒钟之后，你会在终端中看到关于AFNetworking类库的一些信息。
这说明，AFNetworking是支持CocoaPods，所以我们可以利用CocoaPods将AFNetworking导入你的项目中。
