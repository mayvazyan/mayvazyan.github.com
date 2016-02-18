---
layout: post
title: Erlang and web development
date: 2011-09-01 23:15
author: ayvazyan
comments: true
categories: [Erlang, MVC, Uncategorized]
---
First off all what is Erlang? Here’s description from the <a href="http://www.erlang.org/">http://www.erlang.org/</a>
<blockquote>Erlang is a programming language used to build massively scalable soft real-time systems with requirements on high availability. Some of its uses are in telecoms, banking, e-commerce, computer telephony and instant messaging. Erlang's runtime system has built-in support for concurrency, distribution and fault tolerance</blockquote>
First time I heard about Erlang was way back into <abbr>2007. At that time I thought about it as a great choice for development of the server applications such as game servers, instant messaging, etc. </abbr>

<abbr>Recently I was wondering if are there any Erlang frameworks for web development exists. And as you probably expected there are Many frameworks. I made some research of the <a href="http://www.chicagoboss.org/">Chicago Boss</a>. And you know it’s just awesome! One of the greatest features is <em>Zero downtime code upgrades in production.</em></abbr>

I’m sure Chicago Boss doesn’t so mature as for example ASP.NET. But you know ASP.NET is a general solution. You can build any kind of web application using it. It could be regular HTML pages or highly interactive single-page application or just web service. I suppose Erlang (and Chicago Boss) are more specialized. For example if I plan to build web site with regular HTML pages I probably will rely on ASP.NET (or PHP). But for single-page applications with requirements on high availability I will consider Erlang (Chicago Boss) + HTML5 (jQuery, Knockout)
