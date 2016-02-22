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

```
[String.Format(&amp;quot;/p:SkipInvalidConfigurations=true {0}&amp;quot;, MSBuildArguments)]
```
And replace it by the following text:

```
[String.Format(&amp;quot;/p:SkipInvalidConfigurations=true /p:BuildNumber={1} /p:RevisionNumber={2} {0}&amp;quot;, MSBuildArguments, BuildDetail.BuildNumber.Substring(BuildDetail.BuildNumber.LastIndexOf(&amp;quot;.&amp;quot;) + 1), BuildDetail.SourceGetVersion.Substring(1))]
```

MSBuild script should looks similar to:

```xml
<PropertyGroup>
    <BuildNumber Condition="'$(BuildNumber)' == ''">0</BuildNumber>
    <RevisionNumber Condition="'$(RevisionNumber)' == ''">0</RevisionNumber>
  </PropertyGroup>

  <PropertyGroup>
    <Major>1</Major>
    <Minor>0</Minor>
    <Build>$(BuildNumber)</Build>
    <Revision>$(RevisionNumber)</Revision>
  </PropertyGroup>
```
