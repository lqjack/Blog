---
layout: post
title: Mac下搭建jekyll环境 
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Tools
star: true
category: blog
author: Jack
description: Jekyll环境搭建
---



# 1、安装/升级本地ruby
## 安装rvm

可以先 ruby -v 查看下本地ruby版本号，经多次尝试使用ruby2.0.0版本可以正常使用。

网上不少人使用源码安装来替换本地ruby，其实用rvm来管理多版本ruby是更安全、方便的方案。rvm的安装比较简单：
```shell
	curl -L https://get.rvm.io | bash -s stable
```

安装好rvm后需要按照提示 
```shell 
	source ~/.bash_profile
``` 
将rvm添加到环境变量中。

安装ruby
接下来可以正式安装ruby了，这里可以先通过 rvm use 命令来获取详细的版本号，安装过程可参考以下代码：


```shell
	rvm install ruby -v 2.0
````


当出现错误：
Can't install RMagick 2.13.1. Can't find MagickWand.h.
*** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of
necessary libraries and/or headers.  Check the mkmf.log file for more
details.  You may need configuration options.

请尝试以下操作：
It looks like ImageMagick 7 changed include file path.

On building rmagick, since it includes file as wand/MagickWand.h There are no workarounds. It looks like sticking with ImageMagick 6 for now.

On Mac OS X (I tested on Sierra), I used HomeBrew's versions tap like:

brew tap homebrew/versions
brew install imagemagick@6
Then, use the path showen on above installation:

PKG_CONFIG_PATH=/usr/local/opt/imagemagick@6/lib/pkgconfig gem install rmagick
To install with ImageMagick 6.


# 2、安装jekyll

```shell
	gem install jekyll
```

# 3、测试
安装完成后，切换到项目根目录，运行
```shell
	jekyll server(s)
```
,可以通过localhost:4000访问。

