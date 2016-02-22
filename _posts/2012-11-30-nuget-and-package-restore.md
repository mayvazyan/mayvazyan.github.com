---
layout: post
title: NuGet + Package Restore = Failed Build?
date: 2012-11-30 20:07
author: ayvazyan
comments: true
categories: [.NET, Continuous Integration, nuget]
---

<p>Recently we faced weird issue with NuGet. Then we build our solution (with Package Restore enabled) build fails due to the NuGet error.</p>

<p>We have some packages from the internal NuGet server, hence in NuGet.targets we had this:

```xml
<!-- Package sources used to restore packages. By default will used the registered sources under %APPDATA%\NuGet\NuGet.Config -->
<packagesources>
&quot;https://nuget.org/api/v2/;http://ournuget.com/nuget&quot;
</packagesources>
```

NuGet output was:
```One or more errors occurred```

The command was:
```
"c:\ProjectPath\.nuget\nuget.exe" install "c:\ProjectPath\Source\ProjectName\packages.config" -source "https://nuget.org/api/v2/;http://ourinternalnugetserver.com/nuget" -o "c:\ProjectPath\packages"
```

<p>What’s interesting if you run NuGet with empty <em>-source</em> you get nice warning:</p>
<blockquote>WARNING: The schema version of 'Rx-PlatformServices' is incompatible with version 1.8.30524.9000 of NuGet. Please upgrade NuGet to the latest version from <a href="http://go.microsoft.com/fwlink/?LinkId=213942">http://go.microsoft.com/fwlink/?LinkId=213942</a>.
</blockquote>
*I got above warning after executing below command

```
"c:\ProjectPath\.nuget\nuget.exe" install "c:\ProjectPath\Source\ProjectName\packages.config" -source "" -o "c:\ProjectPath\packages"
```


<p>Next steps are obvious “nuget update –self” did the trick.</p>

```
nuget update –self
```
