---
layout: post
title: Migration to TFS 2012
date: 2012-11-18 16:40
author: ayvazyan
comments: true
categories: [Productivity, Source Control, tfs]
---
Over weekends I worked on migration from TFS 2010 to TFS 2012 + SharePoint 2013. Migration process was pretty straightforward, thanks to TFS and SharePoint teams!

During migration I found that some TFS databases are really huge. The answer was that TFS saves all the test binaries, results and code coverage data right inside TFS database (!). For me it was a big surprise.

So I had to use <a href="http://visualstudiogallery.msdn.microsoft.com/3d37ce86-05f1-4165-957c-26aaa5ea1010">Test Attachment Cleaner</a> tool to cleanup all those unnecessary data from TFS:

```
"C:\Program Files\Microsoft Team Foundation Server 2010 Power Tools\Test Attachment Cleaner\tcmpt.exe" attachmentcleanup /collection:"http://tfs.example.com:8080/tfs/Collection" /teamproject:"Team Project" /settingsfile:tfscleanup.settings.txt /outputfile:tfscleanup.logs /mode:delete
```

cleanup.settings.txt contained the following settings:

```xml
<DeletionCriteria>
    <TestRun >
        <AgeInDays OlderThan="30" />
    </TestRun>
    <Attachment>
        <Extensions>
            <Include value="tr_"/>
            <Include value="tlk"/>
            <Include value="dll"/>
            <Include value="exe"/>
            <Include value="pdb"/>
            <Include value="xml"/>
            <Include value="coverage"/>
            <Include value="config"/>
            <Include value="iTrace"/>
            <Include value="wmv"/>
        </Extensions>
    </Attachment>
    <LinkedBugs>
        <Exclude state="Active" />
        <Exclude state="Resolved" />
    </LinkedBugs>
</DeletionCriteria>
```

It did the trick. But I had to shrink database cause test attachments were more than 70% of it's size.
Next I used script from <a href="http://msdn.microsoft.com/en-us/library/ms177571.aspx" title="DBCC INDEXDEFRAG">MSDN</a> to rebuild all indexes.

So if your Build Servers run unit tests, it makes sense to review your TFS databases ;)
