---
layout: post
title: Smart Screen & EV Code Signing
date: 2016-01-31 19:31
author: ayvazyan
comments: true
categories: [.NET, Uncategorized]
---
Recently our QA team started to get "<strong>Windows protected your PC</strong>" messages from the Windows SmartScreen. They saw that message each time they launch the app I'm working on at the moment.
That warning message even didn't display the Publisher correctly. 

We were able to make Smart Screen to show Publisher correctly by signing our application by the SHA-256 code signing certificate (we used SHA-1 originally). 

As for the warning message itself, we had to buy <strong>Extended Validation Code Signing Certificate</strong> to get rid of it.

I want to note that you can keep using <em>signtool.exe</em> to sign binaries. But you can't do that from the automated build scripts because you have to provide a password. That's why we had to update our deployment strategy to make this to work. We added manual intervention step (we are using <a href="https://octopus.com/" title="Octopus Deploy">Octopus</a> by the way) which allows us to sign binaries (by running a script and providing password). More details at <a href="http://stackoverflow.com/questions/17927895/automate-extended-validation-ev-code-signing" title="Automate Extended Validation (EV) code signing">stackoverflow</a>

Also mage.exe didn't play well with EV Code Signing certificate - it didn't ask for the password. As a result manifest was not signed correctly.

Just in case here's the warning message we were getting:


```
<strong>Windows protected your PC</strong>
Windows SmartScreen prevented an unrecognized app from starting. Running this app might put your PC at risk

App: {OurAppName}.exe
Publisher: Unknown
```

