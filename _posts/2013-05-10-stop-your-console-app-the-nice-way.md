---
layout: post
title: Stop your console app the nice way
date: 2013-05-10 16:34
author: ayvazyan
comments: true
categories: [.NET]
---
This would be obvious for someone. Posting it just in case :)

```csharp
    class Program
    {
        private static readonly AutoResetEvent AutoResetEvent = new AutoResetEvent(false);
 
        static void Main(string[] args)
        {
            Console.CancelKeyPress += OnCancelKeyPress;
 
            //TODO: do work here
            AutoResetEvent.WaitOne();
            //TODO: shutdown here
        }
 
        private static void OnCancelKeyPress(object sender, ConsoleCancelEventArgs e)
        {
            e.Cancel = true;
            AutoResetEvent.Set();
        }
    }
```
