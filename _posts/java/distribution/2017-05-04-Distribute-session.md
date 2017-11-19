---
layout: post
title: 分布式Session
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Java
- distribution
star: true
category: blog
author: Jack
description: 分布式环境下Session管理
---

# 1、Session生命周期
---

## 创建
Session创建再服务端，当请求JSP,Servlet时候才会创建（包含SessionId)，默认情况下服务端会将JSESSIONID通过Cookie发送给客户端，一般maxAge属性为-1,表示仅对当前浏览器有效，各个浏览器窗口不共享，关闭浏览器就会失效。因此同一机器的两个浏览器窗口访问服务器时，会生成两个不同的Session。但是由浏览器窗口内的链接、脚本等打开的新窗口（也就是说不是双击桌面浏览器图标等打开的窗口）除外。这类子窗口会共享父窗口的Cookie，因此会共享一个Session。只访问HTML,图片等静态资源不会创建。

注意：新开的浏览器窗口会生成新的Session，但子窗口除外。子窗口会共用父窗口的Session。例如，在链接上右击，在弹出的快捷菜单中选择"在新窗口中打开"时，子窗口便可以访问父窗口的Session。


再次访问时候，会将JSESSIONID放置在请求头中发送。Session根据该Cookie值是否同一用户。

```Java
	request.getSession(true);
```
若包含参数true,服务器会先从请求中查看是否包含sessionId。若找到对应的Session则直接返回，否则创建一个新的session对象。
若参数为false,若找不到sessionId对应的对象，则返回null。


若用户禁用Cookie时候，不能通过服务端通过客户端保存SessionID，可以通过URL重写或者隐藏字段发送请求。可以使用以下语句是否为true,判断客户端是否启用Cookie:
```JavaScript
	navigator.cookieEnabled
```

## 销毁
设置Session超时时间有以下三种方式：

1. 方法体内的参数interval为秒。 
```Java
HttpSession ses = request.getSession();
session.setMaxInactiveInterval(interval);
```


2. web.xml里配置如下信息
```XML
	<session-config>
		<session-timeout>时间长度（单位为分钟）</session-timeout>
	</session-config>
```


3. 在tomcat/conf/server.xml中定义defaultSessionTimeOut=时间长度（分钟），默认是30分钟。
三种方式中当值为-1时，session永不失效。优先级：(1)>(2)>(3)。

- 服务器会把超时的session进行清除。
- 调用session.invalidate()。
- 服务器进程被停止.


# 2、Cookie应用
---

## 如何使用cookie检测初访者
+ 调用HttpServletRequest.getCookies()获取Cookie数组
+ 在循环中检索指定名字的cookie是否存在以及对应的值是否正确
+ 如果是则退出循环并设置区别标识
+ 根据区别标识判断用户是否为初访者从而进行不同的操作

## 使用cookie检测初访者的常见错误
*	不能仅仅因为cookie数组中不存在在特定的数据项就认为用户是个初访者。如果cookie数组为null，客户可能是一个初访者，也可能是由于用户将cookie删除或禁用造成的结果。
*	但是，如果数组非null,也不过是显示客户曾经到过你的网站或域，并不能说明他们曾经访问过你的servlet。其它servlet、JSP页面以及非Java Web应用都可以设置cookie，依据路径的设置，其中的任何cookie都有可能返回给用户的浏览器。
*	正确的做法是判断cookie数组是否为空且是否存在指定的Cookie对象且值正确。

## 使用cookie属性的注意问题
*	属性是从服务器发送到浏览器的报头的一部分；但它们不属于由浏览器返回给服务器的报头。　
*	因此除了名称和值之外，cookie属性只适用于从服务器输出到客户端的cookie；服务器端来自于浏览器的cookie并没有设置这些属性。　
*	因而不要期望通过request.getCookies得到的cookie中可以使用这个属性。这意味着，你不能仅仅通过设置cookie的最大时效，发出它，在随后的输入数组中查找适当的cookie,读取它的值，修改它并将它存回Cookie，从而实现不断改变的cookie值。

## 如何使用cookie记录各个用户的访问计数
* 获取cookie数组中专门用于统计用户访问次数的cookie的值
* 将值转换成int型
* 将值加1并用原来的名称重新创建一个Cookie对象
* 重新设置最大时效
* 将新的cookie输出

