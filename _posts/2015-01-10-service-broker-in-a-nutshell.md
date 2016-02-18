---
layout: post
title: Service Broker in a nutshell
date: 2015-01-10 14:04
author: ayvazyan
comments: true
categories: [Books, MSSQL]
---
Lately I was looking into different Queuing Technologies to choose the best fit for the upcoming project.
In that post I just want to summarize my finding.

I was already familiar with <a href="http://azure.microsoft.com/en-us/services/service-bus/">Azure Service Bus</a> and <a href="http://www.rabbitmq.com/">Rabbit MQ</a>.
But we didn't need advanced routing capabilities they both provide, hence I decided to look into alternative solutions. By the way here's a very nice <a href="http://geekswithblogs.net/michaelstephenson/archive/2012/08/12/150399.aspx">Service Bus for Windows Server &amp; RabbitMQ comparison</a>.

We were already using MS SQL Server to persist the data. So using <a href="http://msdn.microsoft.com/en-us/library/bb522893.aspx">Service Broker</a> was an appealing choice from the very beginning.

Advantages
<ul>
	<li><span style="line-height: 14px;" data-mce-mark="1">Very easy to backup/restore</span></li>
	<li>Sequential Delivery &amp; Related Messages Locking (plus it allows to access internal Sequence ID &amp; Sequence Number)</li>
</ul>
Disadvantages
<ul>
	<li>To en-queue message you should have a <strong>conversation</strong> first. It means you en-queue message into one queue and listen for messages to appear on <strong>another</strong> <strong>queue</strong></li>
	<li><span style="line-height: 14px;" data-mce-mark="1">Index fragmentation then <a href="http://rusanu.com/2010/03/09/dealing-with-large-queues/">Dealing with Large Queues</a></span></li>
</ul>
Alternative solution is to <a href="http://rusanu.com/2010/03/26/using-tables-as-queues/">use tables as queues</a>. The main disadvantage of it is the lack of Activation. Which means you will have to Pull messages from the queue. While Service Broker, Rabbit MQ and others provide Push mechanism to notify listeners about newly added items.

I highly recommend you to read in-death book on Service Broker <a style="line-height: 1.714285714; font-size: 1rem;" href="http://www.amazon.com/Server-Service-Broker-Books-Professionals/dp/1590599993">Pro SQL Server 2008 Service Broker </a> so you will know better in which cases you can leverage Service Broker capabilities.
