---
layout: post
title: Typed XML programming
date: 2013-04-20 16:12
author: ayvazyan
comments: true
categories: [.NET, linq, Open Source, xml, xsd]
---
I want to tell you about very useful project <a href="https://linqtoxsd.codeplex.com/">LINQ to XSD</a>

<blockquote>
The LINQ to XSD technology provides .NET developers with support for typed XML programming. LINQ to XSD contributes to the LINQ project (.NET Language Integrated Query); in particular, LINQ to XSD enhances the existing LINQ to XML technology.
</blockquote> 

Please consider the following code:

```csharp
services services = services.Load(@"c:\services.xml");
string name = services.service.First(x => x.FullTypeName == "xx").Namespace;
```

As you probably understand it reads XML underneath. But you deal with LINQ query and don’t worry about parsing XML.
