---
layout: post
title: "Using Data Contracts: be aware!"
date: 2009-09-14 17:22
author: ayvazyan
comments: true
categories: [.NET]
---
Just another "have to know" thing.
<!--more-->
<blockquote>During deserialization, an uninitialized object is first created, without calling any constructors on the type. Then all data members are deserialized</blockquote>
Please read <a href="http://msdn.microsoft.com/en-us/library/ms733127.aspx">MSDN article</a> for more details.

I'm so wondering: why did they do things working this way?..

Anyway, if you also want to create object without calling it's constructor, just use <a href="http://msdn.microsoft.com/en-us/library/system.runtime.serialization.formatterservices.getuninitializedobject.aspx">FormatterServices.GetUninitializedObject</a>
