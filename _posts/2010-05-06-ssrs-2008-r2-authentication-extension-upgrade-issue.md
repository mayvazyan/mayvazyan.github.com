---
layout: post
title: "SSRS 2008 R2: Authentication Extension (upgrade issue)"
date: 2010-05-06 10:56
author: ayvazyan
comments: true
categories: [MSSQL]
---
Recently we have to upgrade our MS SQL Server 2008 to R2. After upgrade we met a problem - our custom authentication extension stopped to work.
We were able to login to Reporting Service directly, but unable to login to Reports Manager. Also our system was unable to login using ReportExecution2005.asmx service.
After hours of testing and research I've found a workaround at <a href="http://social.msdn.microsoft.com/Forums/en/sqlkjreportingservices/thread/85b20ed6-dab5-4cec-9b55-72f687f4e7b9">social.msdn.microsoft.com</a>. 
I've created HttpModule described in NialoIreland's latest comment (posted on Monday, February 22, 2010 10:54 AM). And authentication started to work correctly!


