---
layout: post
title: Let's Encrypt or HTTPS for everyone
date: 2018-06-09 16:49
author: ayvazyan
comments: true
categories: [I recommend]
---

It's a year since we are using free certificates on some of our production servers. 
So I decided to put together a tiny article highlighing how easy is to make connections to your server secure using [Let's Encrypt](https://letsencrypt.org/):


#### Let's Encrypt
`To enable HTTPS on your website, you need to get a certificate (a type of file) from a Certificate Authority (CA). Let’s Encrypt is a CA. In order to get a certificate for your website’s domain from Let’s Encrypt, you have to demonstrate control over the domain. With Let’s Encrypt, you do this using software that uses the ACME protocol, which typically runs on your web host.
`

More details at https://letsencrypt.org/getting-started/


#### ACME Client for Windows - win-acme


To enable HTTPS on IIS website all you have to do is below 3 steps:
1. Find out Site ID in IIS (Open IIS Manager and click on the "Sites" folder)
2. Download a [Simple ACME Client for Windows](https://github.com/PKISharp/win-acme/releases)
3. Run ACME Client (letsencrypt.exe) passing Site ID and Email for notifications

For example if you Site ID is 1 and email for notifications is john.doe@example.com the command will look like this:
`
letsencrypt.exe --plugin iissite --siteid 1 --emailaddress john.doe@example.com --accepttos --usedefaulttaskuser
`
