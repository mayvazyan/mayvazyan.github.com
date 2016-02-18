---
layout: post
title: Structured Logging
date: 2014-07-22 23:20
author: ayvazyan
comments: true
categories: [.NET, I recommend]
---
<span style="line-height: 1.714285714; font-size: 1rem;">On weekends I was reading latest <a href="http://assets.thoughtworks.com/assets/technology-radar-july-2014-en.pdf">Technology Radar from Thought Works</a></span><span style="line-height: 1.714285714; font-size: 1rem;">.</span>

It’s really interesting! Some of things they mentioned we are already using here at Compellotech (such as HAL, Angular JS, Nancy, TypeScript, etc.) Others are good not know about, for example Structured Logging.

<i>Structured Logging</i>

Lately I was thinking on the best approach to enabled monitoring in our distributed system. The goal is to have some universal solution which will allow us to release something in 1 or 2 sprints (we use one week sprint).

I did some research and I suppose it’s a way to go for us.
<ul>
	<li>Allows to enable monitoring in all the components without significant changes</li>
	<li>Allow to setup Alerts for different things (if they appear in the log)</li>
	<li>Allow to search for issues for example by Customer ID. Just imagine you type CustomerID=”777” and you see all the events in the system related to that customer!</li>
</ul>
<i>Technical details</i>

There is a great Structured Logging framework <a href="http://serilog.net/">http://serilog.net/</a>. It allows you to publish logs to different systems. For example you would use <a style="line-height: 1.714285714; font-size: 1rem;" href="https://getseq.net/">Seq</a> web application. Alternative approach is to publish logs to Elastic Search and use Kibana as a Front End. Another interesting option is to push logs into MongoDB. So you 'll be able to do something like  <b style="line-height: 1.714285714; font-size: 1rem;">db.log.find( { customerId: “777”, application: “PaymentGateway” } )</b>
