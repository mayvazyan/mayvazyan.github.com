---
layout: post
title: WatiN - Web Application Testing
date: 2010-03-11 13:24
author: ayvazyan
comments: true
categories: [.NET, I recommend, TDD, BDD, etc.]
---
I would like to recommend you an amazing testing framework - <strong>WatiN</strong>. If can make Web Application Testing to be the easiest thing in a world :)
<!--more-->
Don't believe me? Just review the following example which does searching on Google.

More info available on the <a href="http://watin.sourceforge.net/index.html">WatiN's official site</a>.
<code>
[Test] 
public void SearchForWatiNOnGoogle()
{
 using (var browser = new IE("http://www.google.com"))
 {
  browser.TextField(Find.ByName("q")).TypeText("WatiN");
  browser.Button(Find.ByName("btnG")).Click();
  
  Assert.IsTrue(browser.ContainsText("WatiN"));
 }
}</code>
