---
layout: post
title: "Team City: Windows Authentication"
date: 2011-10-14 10:15
author: ayvazyan
comments: true
categories: [Continuous Integration, TeamCity, Windows Authentication, Windows Domain]
---
<p>There is detailed article on how to <a href="http://confluence.jetbrains.net/display/TCD65/Configuring+Authentication+Settings">configure different authentication modes</a> in Team City.</p>  <p>But it lacks some information…</p>  <p>Let consider the following example:</p>  <ol>   <li>You setup Team City</li>    <li>Configured Project in it</li>    <li>All went fine and now you need to configure user access</li>    <li>So you switched Team City to Windows Authentication</li>    <li>Now you can login with you Domain credentials, but you can’t give administrator rights to any user since you don’t have administrator yet</li> </ol>  <p>So I found the following workaround:</p>  <ol>   <li>Login using Default Authentication Mode as Administrator in the Browser #1</li>    <li>Switch Authentication Mode to Windows Authentication</li>    <li>Login in as a Windows Domain User in the Browser #2</li>    <li>In the Browser #1 open Users and Groups</li>    <li>You will see newly created user account for Windows Domain User logged in using Browser #2</li>    <li>You can select this account and give it administrative rights</li> </ol>
