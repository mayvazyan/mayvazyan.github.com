---
layout: post
title: Notes about temporary tables support in MSSQL
date: 2009-10-12 17:08
author: ayvazyan
comments: true
categories: [MSSQL, MSSQL]
---
MSSQL provides wide abilities to use it's temporary tables.

<strong>I. Visible locally.</strong>
<blockquote>declare @SomeTableName table (
Id int,
Title nvarchar(50)
);

create table #SomeTableName (
Id int,
Title nvarchar(50)
)</blockquote>
Note that the first table will be in memory (<em>in most cases</em>), but second will be stored in tempDB

<strong>II. Visible to everyone:</strong>
<blockquote>create table ##SomeTableName (
Id int,
Title nvarchar(50)
)</blockquote>
