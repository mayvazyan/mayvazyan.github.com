---
layout: post
title: "TFS 2012 migrated from TFS 2010: Project Creation fails"
date: 2013-02-04
author: ayvazyan
comments: true
categories: [Agile, Source Control]
---
As I mentioned previously we <a href="http://ayvazyan.net/2012/11/migration-to-tfs-2012/">migrated to the TFS 2012 + SharePoint 2013</a>. It’s worth to mention that TFS 2012 is just great! It’s so handy to use new dashboards and task planning stuff. We just Love it <img class="wlEmoticon wlEmoticon-smile" style="border-style: none;" alt="Smile" src="http://ayvazyan.net/wp-content/uploads/2013/02/wlEmoticon-smile.png" />

But today we had to create new project… and it did work for us.

<strong>TF301777: Team Project Creation Failed</strong>

New Team Project Wizard encountered the following error and could not continue.

<strong>Error</strong>

The Project Creation Wizard encountered an error while creating reports to the SQL Server Reporting Services on http://servername/ReportServer/ReportService2005.asmx.

After some Goodling I found <a href="http://www.technologytoolbox.com/blog/jjameson/archive/2010/05/20/reporting-errors-with-tfs-migration-upgrade.aspx">Jeremy Jameson</a> blog post on the similar issue. Although our cause was a bit simpler - all the TFS reports were in Reporting Server. So I just had to ran below SQL statements:


```sql
USE master
GO
GRANT EXECUTE ON master.dbo.xp_sqlagent_notify TO  [NT SERVICE\ReportServer]
GO
GRANT EXECUTE ON master.dbo.xp_sqlagent_enum_jobs TO  [NT SERVICE\ReportServer]
GO
GRANT EXECUTE ON master.dbo.xp_sqlagent_is_starting TO  [NT SERVICE\ReportServer]
GO
USE msdb
GO
-- Permissions for SQL Agent SP's
GRANT EXECUTE ON msdb.dbo.sp_help_category TO  [NT SERVICE\ReportServer]
GO
GRANT EXECUTE ON msdb.dbo.sp_add_category TO  [NT SERVICE\ReportServer]
```
