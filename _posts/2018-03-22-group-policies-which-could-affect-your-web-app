---
layout: post
title: Group Policies which could affect your Web Application
date: 2017-04-23 3:30
author: michael
comments: true
categories: [web]
---

We are working on a web application which heavily depends on the following browsers' features:
- *Application Cache* - it allows websites to ask browser to cache them, so that users are able to open these websites offline.
- *Indexed DB* - it allows websites to store data in the browser cache, so that all needed data will be available offline.
- *Web Storage* - it allows websites to store settings in the browser cache.

### Group Policy

It's common for Enterprises to adjust default *IE 11* settings using Group Policies.
In such cases some of the functionality will not be available. For example website may fail to work offline if it's unable to store data into browser's cache.
We prepared a list of the settings which might have impact on the websites utilizing above browser features.

#### Edge

- *Computer Configuration -> Administrative Template -> Windows Components -> Microsoft Edge*
	- **Allow clearing browsing data on exit.** Not Configured by default. If Enabled could cause a data loss, also users won’t be able to open application offline. 

#### IE 11

- *Computer Configuration -> Administrative Template -> Windows Components -> Internet Explorer -> Internet Control Panel -> Advanced Page*
	- **Empty Temporary Internet Files folder when browser is closed** Disabled by default.
- *Computer Configuration -> Administrative Template -> Windows Components -> Internet Explorer -> Internet Control Panel -> General Page -> Browsing History*
	- **Allow websites to store application caches on client computers.** Enabled by default.
	- **Set application caches expiration time limit for individual domains.** The default is 30 days. 
	- **Set maximum application cache resource list size.** The default value is 1000. 
	- **Set maximum application cache individual resource size.** The default value is 50 MB.
	- **Set application cache storage limits for individual domains.** The default is 50 MB.
	- **Set maximum application caches storage limit for all domains.** The default is 1 GB.
	- **Set default storage limits for websites.** Not Configured by default.
	- **Allow websites to store indexed databases on client computers.** Enabled by default. Required for the application to be available offline.
	- **Set indexed database storage limits for individual domains.** The default is 500 MB.
	- **Set maximum indexed database storage limit for all domains.** The default is 4 GB.
