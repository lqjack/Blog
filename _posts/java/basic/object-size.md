---
layout: draft
title: Object size
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Java
- object attribute
star: true
category: blog
author: Jack
description: Object size 
---

boolean and byte: 1 byte
char and short: 2 bytes
int and float: 4 bytes
long and double: 8 bytes
Object references are 4 (8) bytes in a 32-bit (64-bit) JVM
Arrays follow the same rules; that is, it's an object reference so that takes 4 (or 8) bytes in your object, and then its length multiplied by the size of its element.
