---
layout: post
title: Excel 2007 Automation under Windows Server 2008 x64
date: 2009-10-01 18:40
author: ayvazyan
comments: true
categories: [.NET]
---
Today I've run into the strange problem. I developing a windows service which should generate an Excel files. I've tested it's logic using unit tests and all worked fine.

But then I started testing for the windows service, I saw the following strange error:

<!--more-->

<blockquote>
Exception from HRESULT: 0x800A03EC
---&lt; Exception trace &gt;---
at Microsoft.Office.Interop.Excel.WorkbookClass.SaveAs(Object Filename, Object FileFormat, Object Password, Object WriteResPassword, Object ReadOnlyRecommended, Object CreateBackup, XlSaveAsAccessMode AccessMode, Object ConflictResolution, Object AddToMru, Object TextCodepage, Object TextVisualLayout, Object Local)
Exception from HRESULT: 0x800A03EC
---&lt; Exception trace &gt;---
</blockquote>

So my windows service was unable to save Excel file.

I've checked "Allow service to interact with desktop" option, but the problem was still there...

After some time of googling I've found greate&amp;simple solution in <strong>H Ogawa's </strong><a href="http://social.msdn.microsoft.com/Forums/en-US/innovateonoffice/thread/b81a3c4e-62db-488b-af06-44421818ef91">post</a>. Hurrah!! This guy saved a lot of time for me! Thanks a lot! :)

Just in case you need it here is a solution:



<blockquote>
<strong>Windows 2008 Server x64</strong>
<br>Please create the following folder:
<br>C:WindowsSysWOW64configsystemprofileDesktop
<br><br><strong>Windows 2008 Server x86</strong>
<br>Please create the following folder:
<br>C:WindowsSystem32configsystemprofileDesktop
</blockquote>


