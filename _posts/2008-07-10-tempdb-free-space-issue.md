---
id: 1591
title: 'TempDB Free Space % Opsmgr Issue'
date: 2008-07-10T15:14:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2008/07/10/tempdb-free-space-issue.aspx
permalink: /tempdb-free-space-issue/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1448"
  - "1448"
  - "1448"
  - "1448"
  - "1448"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Uncategorized
---
I just installed Opsmgr @ one of my clients. Using a default setup. One opsmgr server and one SQL 2005 server.

We put the TempDB on a different disk and configured the database as follow:

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="66" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/TempDBFreeSpaceIssue_1019B/image_thumb.png" width="710" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/TempDBFreeSpaceIssue_1019B/image_2.png)

We set a initial fixed size with autogrowth none.

Problem now is that opsmgr is complaining about the free space of our tempDB:

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="301" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/TempDBFreeSpaceIssue_1019B/image_thumb_1.png" width="702" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/TempDBFreeSpaceIssue_1019B/image_4.png)

The value is 0! That was not possible because we just give the TempDB 9gig. So we ran the following query to check ou TempDB size:

SELECT SUM(unallocated\_extent\_page_count) AS [free pages], 

(SUM(unallocated\_extent\_page_count)*1.0/128) AS [free space in MB] 

FROM sys.dm\_db\_file\_space\_usage; 

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="552" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/TempDBFreeSpaceIssue_1019B/image_thumb_2.png" width="645" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/TempDBFreeSpaceIssue_1019B/image_6.png) 

As you can see we still have 8.9 Gig Free Space for our TempDB!! 

&nbsp;

So, we figured out that&nbsp; if you put the TempDB on autogrowth non. The script that checks for DB free space is not working well! The strange thing is that that issue only occure with the TempDB! Opsmgr is not going to complain about the free space of other DB&#8217;s when you put them on autogrowth yes!

&nbsp;

Finally, we put our TempDB on autogrowth:

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="110" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/TempDBFreeSpaceIssue_1019B/image_thumb_3.png" width="546" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/TempDBFreeSpaceIssue_1019B/image_8.png) 

And after a while everything was OK:

&nbsp;

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="551" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/TempDBFreeSpaceIssue_1019B/image_thumb_4.png" width="509" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/TempDBFreeSpaceIssue_1019B/image_10.png) 

Greetz,

Alkin

&nbsp;

ps: THX <a href="http://trycatch.be/blogs/oern/default.aspx" target="_blank">Jeroen </a>for assisting me!