---
layout: post
title: SQL Server Managed Backup to Microsoft Azure
date: 2016-12-22 17:39
author: michael
comments: true
categories: [Open Source]
---

Recently we migrated one of our projects to SQL Server 2016. As part of migration we enabled TDE for some databases. 
Next step was to configure backups.

On our old SQL Server 2008 we already used to backup to Azure. It's very convenient! 
So we were happy to use *Managed Backup* feature of SQL Server 2016.

There is really good step-by-step tutorial on how to setup it on [MSDN](https://msdn.microsoft.com/en-us/library/dn435916.aspx)
I just want to note that then you configure "instance level" backups, keep in mind that you will have to apply the same settings to existing databases manually. So it makes sense to first configure "Instance Level" backup settings and then restore your databases. It might save you a bit of time.

It was a breeze to configure *Managed Backup*... very smooth experience. Highly recommend! 
