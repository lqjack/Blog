---
layout: draft
title: DDD concept
date: 2016-02-24 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- DDD
star: true
category: blog
author: Jack
description: DDD introduction
---


Time Point refers that the date in any precision and time zone issues according to the specfic situation. In the situation ,you can ignore the date issue , and force the attention to bussiness thinss.
Effective : Add a time period to an object to show when it is effective.
Audit Log : A simple log of changes, intended to be easily written and non-intrusive.
Temporal Objec : An object that changes over time. Each version captures the state of the object for some period of time. Any time the value of any property of the object changes, you get a new version. Thus you can imagine the versions as a list of objects with an Effectivity to handle the date range.
Another issue is how the business folks like to see the information. If they want to think of a contact of having explicit amendments, then it's worth using Temporal Object even if only a single property is temporal. As soon as business folks need to refer explicitly to versions, you need Temporal Object to give them versions to refer to.

Snapshot : A view of an object at a point in time

A temporal collection is a simple way to implement a Temporal Property. The basic representation and interface for a temporal collection is similar to a map: provide a get and put operation that uses a date as an index. Indeed a map makes a good backing collection for it.

Parallel Model : Allow an alternative representation of the state of an application, either at a different time or in a hypothetical state.



