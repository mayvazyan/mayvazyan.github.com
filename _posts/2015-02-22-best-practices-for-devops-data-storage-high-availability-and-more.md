---
layout: post
title: Best practices for DevOps, data storage, high availability, and more
date: 2015-02-22 23:21
author: ayvazyan
comments: true
categories: [Books, I recommend]
---
Just read <a href="http://www.microsoftvirtualacademy.com/ebooks#9780735695658" title="Building Cloud Apps with Microsoft Azure">Building Cloud Apps with Microsoft Azure</a>. 
It's available as a free ebook on <em>Microsoft Virtual Academy</em>.
I'd like to say that it was a really interesting reading! 

In my opinion most of the patterns and ideas described in the book could be (and should be!) applied in on-premises as well.
For example 
<ul>

	<li><a href="http://octopusdeploy.com/">Octopus</a> allows you to setup a very nice DevOps workflow on-premises.</li>

	<li>In any .NET application you will benefit from using <a href="https://msdn.microsoft.com/en-us/library/hh191443.aspx">Async/Await</a> approach.</li>

	<li>Any big application should have a good Monitoring and telemetry. I'm personally very happy with <a href="http://serilog.net/">Serilog</a> and <a href="https://github.com/etishor/Metrics.NET/wiki">Metrics.Net</a></li>

	<li>Using Cache is a great idea for most of the applications. I'm a big fan of <a href="http://redis.io/">Redis</a></li>

	<li>Dependency Injection is also a must have in most of applications. I like <a href="https://simpleinjector.org/index.html">Simple Injector</a> very much.</li>

	<li>Queue-centric work pattern also could be applied in on-premises scenario. You would use <a href="http://www.rabbitmq.com/">RabbitMQ</a>, <a href="http://redis.io/commands/rpoplpush">Redis</a>, <a href="http://ayvazyan.net/2015/01/service-broker-in-a-nutshell/">Service Broker</a>, etc. for that purpose</li>

</ul>


