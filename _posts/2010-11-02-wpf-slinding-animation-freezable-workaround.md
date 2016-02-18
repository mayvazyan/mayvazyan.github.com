---
layout: post
title: "WPF: Slinding Animation. 'Freezable' workaround."
date: 2010-11-02 14:30
author: ayvazyan
comments: true
categories: [.NET]
---
While ago I needed to implement an Slide InOut amination in WPF. The first attempt was to set TranslateTransform in Animation (to make the control sliding out if it's content was set to null). But since animations should be freezable I wasn't able to do so.
I googled for a while with no luck. But I found a straightforward solution - I just "inverted" the logic.

<!--more-->

So now by default my control is hidden:
<!-- Start block. Created with Code4Blog for Microsoft Visual Studio 2010. Copyright (c)2010 Vitaly Zayko http://zayko.net -->
<div style="color:black;overflow:auto;width:99.5%;">
<pre style="margin:0;"> <span style="color:#0000ff;">&lt;<span style="color:#a31515;">TranslateTransform</span></span></pre>
<pre style="margin:0;">                                <span style="color:#ff0000;"> Y<span style="color:#0000ff;">="<span style="color:#000000;">{</span><span style="color:#a31515;">Binding<span style="color:#ff0000;"> ActualHeight<span style="color:#0000ff;">,<span style="color:#ff0000;"> RelativeSource<span style="color:#0000ff;">=<span style="color:#000000;">{</span><span style="color:#a31515;">RelativeSource<span style="color:#ff0000;"> AncestorType<span style="color:#0000ff;">=Grid<span style="color:#000000;">}</span><span style="color:#000000;">}</span>"</span></span></span></span></span></span></span></span></span></span></pre>
<pre style="margin:0;">                                <span style="color:#0000ff;"> /&gt;</span></pre>
<pre style="margin:0;"></pre>
</div>
<!-- End block -->
In trigger I just set TranslateTransform to 0. Please review the following example:
<!-- Start block. Created with Code4Blog for Microsoft Visual Studio 2010. Copyright (c)2010 Vitaly Zayko http://zayko.net -->
<div style="color:black;overflow:auto;width:99.5%;">
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;<span style="color:#a31515;">Trigger<span style="color:#ff0000;"> Property<span style="color:#0000ff;">="Content"<span style="color:#ff0000;"> Value<span style="color:#0000ff;">="<span style="color:#000000;">{</span><span style="color:#a31515;">x<span style="color:#0000ff;">:<span style="color:#a31515;">Null<span style="color:#0000ff;"><span style="color:#000000;">}</span>"&gt;</span></span></span></span></span></span></span></span></span></span></span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;<span style="color:#a31515;">Trigger.ExitActions<span style="color:#0000ff;">&gt;</span></span></span></span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;<span style="color:#a31515;">BeginStoryboard<span style="color:#0000ff;">&gt;</span></span></span></span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;<span style="color:#a31515;">Storyboard<span style="color:#0000ff;">&gt;</span></span></span></span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;<span style="color:#a31515;">DoubleAnimation</span></span></span></pre>
<pre style="margin:0;">                                            <span style="color:#ff0000;"> To<span style="color:#0000ff;">="0"</span></span></pre>
<pre style="margin:0;">                                            <span style="color:#ff0000;"> Duration<span style="color:#0000ff;">="00:00:2.1"</span></span></pre>
<pre style="margin:0;">                                            <span style="color:#ff0000;"> Storyboard.TargetName<span style="color:#0000ff;">="PART_Host"</span></span></pre>
<pre style="margin:0;">                                            <span style="color:#ff0000;"> Storyboard.TargetProperty<span style="color:#0000ff;">="(FrameworkElement.RenderTransform).(TranslateTransform.Y)"</span></span></pre>
<pre style="margin:0;">                                            <span style="color:#ff0000;"> FillBehavior<span style="color:#0000ff;">="HoldEnd"</span></span></pre>
<pre style="margin:0;">                                            <span style="color:#0000ff;"> /&gt;</span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;/<span style="color:#a31515;">Storyboard<span style="color:#0000ff;">&gt;</span></span></span></span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;/<span style="color:#a31515;">BeginStoryboard<span style="color:#0000ff;">&gt;</span></span></span></span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;/<span style="color:#a31515;">Trigger.ExitActions<span style="color:#0000ff;">&gt;</span></span></span></span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;<span style="color:#a31515;">Trigger.EnterActions<span style="color:#0000ff;">&gt;</span></span></span></span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;<span style="color:#a31515;">BeginStoryboard<span style="color:#0000ff;">&gt;</span></span></span></span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;<span style="color:#a31515;">Storyboard<span style="color:#0000ff;">&gt;</span></span></span></span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;<span style="color:#a31515;">DoubleAnimation</span></span></span></pre>
<pre style="margin:0;">                                            <span style="color:#ff0000;"> From<span style="color:#0000ff;">="0"</span></span></pre>
<pre style="margin:0;">                                            <span style="color:#ff0000;"> Duration<span style="color:#0000ff;">="00:00:2.1"</span></span></pre>
<pre style="margin:0;">                                            <span style="color:#ff0000;"> Storyboard.TargetName<span style="color:#0000ff;">="PART_Host"</span></span></pre>
<pre style="margin:0;">                                            <span style="color:#ff0000;"> Storyboard.TargetProperty<span style="color:#0000ff;">="(FrameworkElement.RenderTransform).(TranslateTransform.Y)"</span></span></pre>
<pre style="margin:0;">                                            <span style="color:#ff0000;"> FillBehavior<span style="color:#0000ff;">="Stop"</span></span></pre>
<pre style="margin:0;">                                            <span style="color:#0000ff;"> /&gt;</span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;/<span style="color:#a31515;">Storyboard<span style="color:#0000ff;">&gt;</span></span></span></span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;/<span style="color:#a31515;">BeginStoryboard<span style="color:#0000ff;">&gt;</span></span></span></span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;/<span style="color:#a31515;">Trigger.EnterActions<span style="color:#0000ff;">&gt;</span></span></span></span></pre>
<pre style="margin:0;"> <span style="color:#a31515;"> <span style="color:#0000ff;">&lt;/<span style="color:#a31515;">Trigger<span style="color:#0000ff;">&gt;</span></span></span></span></pre>
<pre style="margin:0;"></pre>
</div>
&nbsp;

Hope this can help someone.
