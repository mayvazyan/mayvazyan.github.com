---
layout: post
title: Command Query Responsibility Segregation (CQRS) pattern
date: 2014-07-13 16:44
author: ayvazyan
comments: true
categories: [.NET, I recommend]
---
Time flies, it's more than two years since I <a href="http://ayvazyan.net/2011/12/command-query-responsibility-segregation-cqrs-pattern/">discovered</a> CQRS pattern.

If it's first time you hear about CQRS, there is a great <a href="http://channel9.msdn.com/Events/Patterns-Practices-Symposium-Online/Patterns-Practices-Symposium-Online-2012/A-Journey-into-CQRS" title="A Journey into CQRS">A Journey into CQRS</a> talk on Channel 9.

Today we are using CQRS actively at <a href="http://www.compellotech.com/">Compellotech</a>. We are using it as a high level architecture on some components. In the same time we are using it inside of our systems to make internal design better. 

The approach we are using is Very similar to the one described by <a href="http://www.cuttingedge.it/blogs/steven/pivot/entry.php?id=91">Steven on .NET Junkie</a>. I really encourage you to check his articles out. By the way he's the author of easy, flexible, and fast dependency injection framework - <a href="https://simpleinjector.codeplex.com/">Simple Injector</a>.
