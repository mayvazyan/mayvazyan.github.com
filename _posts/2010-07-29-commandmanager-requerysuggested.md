---
layout: post
title: CommandManager.RequerySuggested
date: 2010-07-29 15:58
author: ayvazyan
comments: true
categories: [.NET]
---
Is the following code seems O.K.?

CommandManager.RequerySuggested += OnCommandManagerRequerySuggested;

void OnCommandManagerRequerySuggested(object sender, EventArgs e)
        {
            ICommand command = Command;
            if (command != null)
                IsEnabled = command.CanExecute(null);
        }

Not really, since CommandManager holds the handlers as a weak reference, we need to have our own strong reference to our delegate.

For example local field:
private readonly EventHandler commandManagerOnRequerySuggested;
