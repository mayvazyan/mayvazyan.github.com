---
layout: post
title: primaryGroupToken via C# from Active Directory (AD)
date: 2012-03-02 16:53
author: ayvazyan
comments: true
categories: [.NET, Active Directory, AD, C#, PowerShell]
---
I needed to change Primary Group of the Active Directory user programmatically (via C#).

I found a good <a href="http://www.indented.co.uk/index.php/2010/01/22/changing-the-primary-group-with-powershell/">example in PowerShell</a>.

But it wasn’t obvious for me on how to convert the following code fragment into C#:

```ps
$NewGroup = [ADSI]"LDAP://CN=Domain Guests,CN=Users,$DomainNC"
$NewGroup.GetInfoEx(@("primaryGroupToken"), 0)
$NewGroupToken = $NewGroup.Get("primaryGroupToken")
```

So <a href="http://social.msdn.microsoft.com/forums/en-US/csharpgeneral/thread/ca0414f5-e447-4d75-9d68-68926580d48d/">here is it</a>, just in case it isn’t obvious for you as well ;)


```csharp
group.Invoke("GetInfoEx", new object[] { new object[] { "primaryGroupToken" }, 0 });
object primaryGroupToken = group.Invoke("Get", new object[] { "primaryGroupToken" });
```
