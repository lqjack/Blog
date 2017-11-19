---
layout: draft
title: MyBatis
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Java
star: true
category: blog
author: Jack
description: MyBatis
---

Mapped Statement is core of Mybatis.


<select
  id="selectPerson"
  parameterType="int"
  parameterMap="deprecated"
  resultType="hashmap"
  resultMap="personResultMap"
  flushCache="false"
  useCache="true"
  timeout="10000"
  fetchSize="256"
  statementType="PREPARED"
  resultSetType="FORWARD_ONLY">


Attribute	Description
id	A unique identifier in this namespace that can be used to reference this statement.
parameterType	The fully qualified class name or alias for the parameter that will be passed into this statement. This attribute is optional because MyBatis can calculate the TypeHandler to use out of the actual parameter passed to the statement. Default is unset.
parameterMap	This is a deprecated approach to referencing an external parameterMap. Use inline parameter mappings and the parameterType attribute.
resultType	The fully qualified class name or alias for the expected type that will be returned from this statement. Note that in the case of collections, this should be the type that the collection contains, not the type of the collection itself. Use resultType OR resultMap, not both.
resultMap	A named reference to an external resultMap. Result maps are the most powerful feature of MyBatis, and with a good understanding of them, many difficult mapping cases can be solved. Use resultMap OR resultType, not both.
flushCache	Setting this to true will cause the local and 2nd level caches to be flushed whenever this statement is called. Default: false for select statements.
useCache	Setting this to true will cause the results of this statement to be cached in 2nd level cache. Default: true for select statements.
timeout	This sets the number of seconds the driver will wait for the database to return from a request, before throwing an exception. Default is unset (driver dependent).
fetchSize	This is a driver hint that will attempt to cause the driver to return results in batches of rows numbering in size equal to this setting. Default is unset (driver dependent).
statementType	Any one of STATEMENT, PREPARED or CALLABLE. This causes MyBatis to use Statement, PreparedStatement or CallableStatement respectively. Default: PREPARED.
resultSetType	Any one of FORWARD_ONLY|SCROLL_SENSITIVE|SCROLL_INSENSITIVE. Default is unset (driver dependent).
databaseId	In case there is a configured databaseIdProvider, MyBatis will load all statements with no databaseId attribute or with a databaseId that matches the current one. If case the same statement if found with and without the databaseId the latter will be discarded.
resultOrdered	This is only applicable for nested result select statements: If this is true, it is assumed that nested results are contained or grouped together such that when a new main result row is returned, no references to a previous result row will occur anymore. This allows nested results to be filled much more memory friendly. Default: false.
resultSets	This is only applicable for multiple result sets. It lists the result sets that will be returned by the statement and gives a name to each one. Names are separated by commas.
