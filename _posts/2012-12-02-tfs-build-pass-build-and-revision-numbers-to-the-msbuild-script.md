---
layout: post
title: TFS Build - pass build and revision numbers to the MSBuild script.
date: 2012-12-02 18:48
author: ayvazyan
comments: true
categories: [.NET, Continuous Integration]
---
If you are using TFS Build as you CI server it's really simple to pass build and revision number to the MSBuild.

Just create a copy of the template you are using at the moment.
And then search for the (there are should be 2 occurrences)
<pre><code>
[String.Format(&amp;quot;/p:SkipInvalidConfigurations=true {0}&amp;quot;, MSBuildArguments)]
</code></pre>
And replace it by the following text:
<pre><code>
[String.Format(&amp;quot;/p:SkipInvalidConfigurations=true /p:BuildNumber={1} /p:RevisionNumber={2} {0}&amp;quot;, MSBuildArguments, BuildDetail.BuildNumber.Substring(BuildDetail.BuildNumber.LastIndexOf(&amp;quot;.&amp;quot;) + 1), BuildDetail.SourceGetVersion.Substring(1))]
</code></pre>

MSBuild script should looks similar to:
<pre><code class=xml>
&lt;PropertyGroup&gt;
    &lt;BuildNumber Condition=&quot;'$(BuildNumber)' == ''&quot;&gt;0&lt;/BuildNumber&gt;
    &lt;RevisionNumber Condition=&quot;'$(RevisionNumber)' == ''&quot;&gt;0&lt;/RevisionNumber&gt;
  &lt;/PropertyGroup&gt;

  &lt;PropertyGroup&gt;
    &lt;Major&gt;1&lt;/Major&gt;
    &lt;Minor&gt;0&lt;/Minor&gt;
    &lt;Build&gt;$(BuildNumber)&lt;/Build&gt;
    &lt;Revision&gt;$(RevisionNumber)&lt;/Revision&gt;
  &lt;/PropertyGroup&gt;
</code></pre>
