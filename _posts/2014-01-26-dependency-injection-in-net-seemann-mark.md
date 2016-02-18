---
layout: post
title: Dependency Injection in .NET. Seemann Mark.
date: 2014-01-26 00:52
author: ayvazyan
comments: true
categories: [.NET, Books]
---
Recently I had a chat with a peer developer about IT books. I recommended him a great <a href="http://blog.ploeh.dk/">Seemann Mark</a>'s book <a href="http://www.manning.com/seemann/">Dependency Injection in .NET</a>. After that I realized that I never blogged about it!

I'd say that in my opinion this is an Must Read book for .NET software developers. At first I was a bit surprised that it's a 500+ pages book about one pattern, but it's really worth it.
First chapters are an amazing explanation of the Dependency Injection and Inversion of Control patterns.
Last chapters dives in details of some popular DI containers. Unfortunately it doesn't contain a chapter about Ninject which is my favorite DI container, but there are tons of information about it on the Internet.

<strong>Service Locator is anti-pattern?</strong>
I was very excited that he lists Service Locator as a DI anti-pattern! We were using Service Locator on a big WPF application couple of years ago. After some time I released that it's not an ideal choice.

Seemann Mark stated the following issues with Service Locator pattern:
<ul>
	<li><span style="line-height: 14px;">The module drags along a redundant Dependency</span></li>
	<li>It isn't apparent that DI is being used</li>
</ul>
I'd like to just add that it's way easier to read the code if you can see all the dependencies just by looking at the class constructor. Also it's easier to test such code because you don't need to configure Service Locator to use Mocks. All you need is just pass the objects you want. In some cases it would be real implementation, in others it would be mock, test double, etc.

So even if you aren't .NET developer I still suppose it makes sense to read first chapters of this amazing book. Highly recommend!

