---
layout: post
title: primaryGroupToken via C# from Active Directory (AD)
date: 2012-03-02 16:53
author: ayvazyan
comments: true
categories: [.NET, Active Directory, AD, C#, PowerShell]
---
<p>I needed to change Primary Group of the Active Directory user programmatically (via C#).</p>  <p>I found a good <a href="http://www.indented.co.uk/index.php/2010/01/22/changing-the-primary-group-with-powershell/">example in PowerShell</a>.</p>  <p>But it wasn’t obvious for me on how to convert the following code fragment into C#:</p>  <p>$NewGroup = [ADSI]&quot;LDAP://CN=Domain Guests,CN=Users,$DomainNC&quot;   <br /><strong>$NewGroup.GetInfoEx(@(&quot;primaryGroupToken&quot;), 0)     <br />$NewGroupToken = $NewGroup.Get(&quot;primaryGroupToken&quot;)</strong></p>  <p>So <a href="http://social.msdn.microsoft.com/forums/en-US/csharpgeneral/thread/ca0414f5-e447-4d75-9d68-68926580d48d/">here is it</a>, just in case it isn’t obvious for you as well <img style="border-bottom-style: none; border-left-style: none; border-top-style: none; border-right-style: none" class="wlEmoticon wlEmoticon-winkingsmile" alt="Winking smile" src="http://ayvazyan.net/wp-content/uploads/2012/03/wlEmoticon-winkingsmile.png" /></p>  <p><strong>group.Invoke(&quot;GetInfoEx&quot;, new object[] { new object[] { &quot;primaryGroupToken&quot; }, 0 });     <br />object primaryGroupToken = group.Invoke(&quot;Get&quot;, new object[] { &quot;primaryGroupToken&quot; });      </strong></p>
