------
layout: post
title: java issue
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Tools
star: true
category: blog
author: Jack
description: java issue
---

# What does “INFO: TLD skipped. URI is already defined” mean?

<p>
*Soulution:* This means that you have duplicate TLD files in your webapp's runtime classpath. As TLDs are normally contained in the library JAR files, this in turn means that you have duplicate JAR files in your webapp's runtime classpath.

Assuming that you haven't touched appserver's /lib folder nor the JDK's /lib folders, then those duplicates are in the /WEB-INF/lib folder of the WAR build. Cleanup it.
</p>

# tomcat-maven-plugin different

1. tomcat7:run	
Runs the current project as a dynamic web application using an embedded Tomcat server. When user run the command may get the error : WebApplicationInitializer cannot cast to 
2. tomcat7:run-war	
Runs the current project as a packaged web application using an embedded Tomcat server.
