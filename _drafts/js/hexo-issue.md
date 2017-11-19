---
layout: draft
title: hexo issue
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Tools
- Hexo
star: true
category: blog
author: Jack
description: hexo issue
---


# hexo g error 

1. stacktree : 
<p>{ [Error: Cannot find module './build/Release/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
{ [Error: Cannot find module './build/default/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
{ [Error: Cannot find module './build/Debug/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }</p>
2. solution : 
<p>

you shoud change the dir to not in the project ,then execute the command as below :
```NodeJs
npm uninstall hexo-cli -g
npm uninstall hexo -g
```

```NodeJs
npm install hexo-cli -g
```
</p>

# hexo deploy error deployer not found git

<p>
install the plugin 
```NodeJs
npm install hexo-deployer-git --save
```
</p>
