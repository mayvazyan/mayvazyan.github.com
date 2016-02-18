---
layout: post
title: Undo/Redo functionality in .NET
date: 2010-01-07 20:48
author: ayvazyan
comments: true
categories: [.NET]
---
You need to implement Undo/Redo functionality? Seems I have something to show you...<!--more-->
I think, that everyone, who needs to implement Undo/Redo functionality in an .NET project should take a look at the great <a href="http://www.codeplex.com/Wikipage?ProjectName=dejavu">DejaVu</a> library.

In short, all that you need is just wrap the fields by <strong>UndoRedo</strong> Generic class. And after that you'll be able to use <strong>DejaVu's</strong> transaction mechanizm

<code>
//Field declaration
class MyData
{
    private readonly UndoRedo name = new UndoRedo("");

    public string string Name
    {
        get { return name.Value; }
        set { name.Value = value; }
    }
//...
}

// Usage exampe.
// NOTE: Exceptions will be handled correctly since in case of exception UndoRedoManager.Cancel() method will be called.
using (UndoRedoManager.Start("My Command"))
{
    UndoRedoManager.Commit();
}
</code>
