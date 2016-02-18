---
layout: post
title: Typed XML programming
date: 2013-04-20 16:12
author: ayvazyan
comments: true
categories: [.NET, linq, Open Source, xml, xsd]
---
<p>I want to tell you about very useful project <a href="https://linqtoxsd.codeplex.com/">LINQ to XSD</a></p>  <blockquote>   <p>The LINQ to XSD technology provides .NET developers with support for typed XML programming. LINQ to XSD contributes to the LINQ project (.NET Language Integrated Query); in particular, LINQ to XSD enhances the existing LINQ to XML technology.</p> </blockquote>  <p>Please consider the following code:</p> 
[code lang="csharp"]
services services = services.Load(@&amp;quot;c:\services.xml&amp;quot;);
string name = services.service.First(x =&amp;gt; x.FullTypeName == &amp;quot;xx&amp;quot;).Namespace;
[/code]
<p>As you probably understand it reads XML underneath. But you deal with LINQ query and don’t worry about parsing XML.</p>
