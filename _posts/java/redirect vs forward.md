---
layout: draft
title: Redirect vs Forward
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Http
star: true
category: blog
author: Jack
description: Redirect vs Forward
---

redirect will respond with a 302 and the new URL in the Location header; the browser/client will then make another request to the new URL
forward happens entirely on a server side; the Servlet container forwards the same request to the target URL; the URL won’t change in the browser
