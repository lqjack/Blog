---
layout: post
title: Build Indigo theme
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Tools
star: true
category: blog
author: Jack
description: Indigo theme
---



# 安装Bundle

For Mac Platform, should do as below [Install nokogiri](http://www.nokogiri.org/tutorials/installing_nokogiri.html).

```ruby
    gem update --system
    xcode-select --install # Then agree to the terms, even if you have done this before!
```

After that , install nokogiri. 

```
    gem install nokogiri
```

When cannot install , please try the code as below:

```ruby
    brew unlink xz
    gem install nokogiri # or bundle install
    brew link xz
```
