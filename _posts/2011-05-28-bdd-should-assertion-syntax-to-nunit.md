---
layout: post
title: BDD .Should() assertion syntax to NUnit
date: 2011-05-28 13:56
author: ayvazyan
comments: true
categories: [.NET, TDD, BDD, etc.]
---
If you didn’t have a chance to review <a href="https://github.com/remi/NUnit.Should">NUnit.Should</a> library you definitely need to do that right now! (it’s available as NuGet Library Package as well)

NUnit.Should adds fancy BDD style syntax to NUnit. For example you could use <strong>5.Should(Be.EqualTo(5))</strong> instead of <strong>Assert.That(5, Is.EqualTo(5))</strong>.
