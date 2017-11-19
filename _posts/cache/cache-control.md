---
layout: post
title: Cache
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Cache
star: true
category: blog
author: Jack
description: Cache
---

> Cache-Control指定了请求和响应遵循的缓存机制。好的缓存机制可以减少对网络带宽的占用，可以提高访问速度，提高用户的体验，还可以减轻服务器的负担。


# Cache-Control主要有以下几种类型：

## (1) 请求Request：

1. no-cache  <p> 不要读取缓存中的文件，要求向WEB服务器重新请求</p>
2. max-age： <p> 表示当访问此网页后的max-age秒内再次访问不会去服务器请求，其功能与Expires类似，只是Expires是根据某个特定日期值做比较。一但缓存者自身的时间不准确.则结果可能就是错误的，而max-age,显然无此问题.。Max-age的优先级也是高于Expires的。</p>
3. max-stale  <p> 允许读取过期时间必须小于max-stale 值的缓存对象。 </p>
4. min-fresh <p> 接受其max-age生命期大于其当前时间 跟 min-fresh 值之和的缓存对象</p>
5. only-if-cached <p> 告知缓存者,我希望内容来自缓存，我并不关心被缓存响应,是否是新鲜的.</p>
6. no-transform   <p> 告知代理,不要更改媒体类型,比如jpg,被你改成png.</p>
7. no-store    <p> 请求和响应都禁止被缓存</p>


## (2) 响应Response：

1. public    <p> 数据内容皆被储存起来，就连有密码保护的网页也储存，安全性很低</p>
2. private    <p> 数据内容只能被储存到私有的cache，仅对某个用户有效，不能共享</p>
3. no-cache    <p> 可以缓存，但是只有在跟WEB服务器验证了其有效后，才能返回给客户端</p>
4. no-store  <p> 请求和响应都禁止被缓存</p>
5. max-age：   <p> 本响应包含的对象的过期时间</p>
6. Must-revalidate    <p> 如果缓存过期了，会再次和原来的服务器确定是否为最新数据，而不是和中间的proxy</p>
7. max-stale  <p>  允许读取过期时间必须小于max-stale 值的缓存对象。</p> 
8. proxy-revalidate  <p> 与Must-revalidate类似，区别在于：proxy-revalidate要排除掉用户代理的缓存的。即其规则并不应用于用户代理的本地缓存上。</p>
9. s-maxage  <p> 与max-age的唯一区别是,s-maxage仅仅应用于共享缓存.而不应用于用户代理的本地缓存等针对单用户的缓存. 另外,s-maxage的优先级要高于max-age.</p>
10. no-transform   <p> 告知代理,不要更改媒体类型,比如jpg,被你改成png.</p>
