---
id: 566
title: 'Optimizing the performance of  your Opsmgr Console and reducing DB size'
date: 2009-05-28T09:12:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2009/05/28/optimizing-the-performance-of-your-opsmgr-console-and-reducing-db-size.aspx
permalink: /optimizing-the-performance-of-your-opsmgr-console-and-reducing-db-size/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1932"
  - "1932"
  - "1932"
  - "1932"
  - "1932"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Database
  - Grooming
  - Issue
  - Opsmgr Console
  - Opsmgr DB
  - sql
---
I had troubles with the Opmsgr Console performance at serveral clients.

One of the most important things to boost your console performance is to reduce the Opsmgr DB size.

&nbsp;

If you want to know which tabel is taking most of your DB size run the following query:

**Simple query to display large tables, to determine what is taking up space in the database:**

SELECT so.name,  
8 * Sum(CASE WHEN si.indid IN (0, 1) THEN si.reserved END) AS data_kb,  
Coalesce(8 * Sum(CASE WHEN si.indid NOT IN (0, 1, 255) THEN si.reserved END), 0) AS index_kb,  
Coalesce(8 * Sum(CASE WHEN si.indid IN (255) THEN si.reserved END), 0) AS blob_kb  
FROM dbo.sysobjects AS so JOIN dbo.sysindexes AS si ON (si.id = so.id)  
WHERE &#8216;U&#8217; = so.type GROUP BY so.name&nbsp; ORDER BY data_kb DESC

[<img height="196" width="244" src="http://scug.be/scom/files/2012/06/clip_image001_thumb_5AEAC222.jpg" alt="clip_image001" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image001_6209FE9A.jpg)

&nbsp;

In my case the localizedtable was taking most of the disk space. Kevin Holman already blogged about this: [http://blogs.technet.com/kevinholman/archive/2008/10/13/does-your-opsdb-keep-growing-is-your-localizedtext-table-using-all-the-space.aspx](http://blogs.technet.com/kevinholman/archive/2008/10/13/does-your-opsdb-keep-growing-is-your-localizedtext-table-using-all-the-space.aspx "http://blogs.technet.com/kevinholman/archive/2008/10/13/does-your-opsdb-keep-growing-is-your-localizedtext-table-using-all-the-space.aspx")&nbsp;

&nbsp;

I followed his procedure, I will describe all the steps I did and has to say I was really suprise by the results! 🙂

&nbsp;

  * Count the rows in the localizedtable

select count(*) from localizedtext

[<img height="244" width="233" src="http://scug.be/scom/files/2012/06/clip_image002_thumb_48A1FB60.jpg" alt="clip_image002" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image002_16AA5AD6.jpg)

In a normal environment with the typical management packs imported the total count of rows should be around the million. In one of my environments it was 22 milion!! So I defenitely needed to clean up this localizedtable!

&nbsp;

  * Look at the most common events in the localized table

select messageid, ltvalue, count(*) as Count from publishermessages with(nolock)  
inner join localizedtext with(nolock)  
on messagestringId = localizedtext.ltstringid  
group by messageid, ltvalue  
order by Count DESC

&nbsp;

In my case it was the exchange management pack that produced the most ammount of events.

&nbsp;

  * Run the clean up script

Kevin Holman has provided a script to clean up the localized table. You can download it from his blog [DeletePublisherMessages.zip](http://blogs.technet.com/kevinholman/attachment/3135933.ashx) .

Notice that this script is NOT supported by Microsoft, as it has not been thoroughly tested!&nbsp; I&rsquo;ve run the script in several environments now and didn&rsquo;t run into issues but as a good Sys admin be carefull and take a backup of your opsmgr DB before running the script. Also make sure that your TEMPDB has enough space. And with enough space I really mean ENOUGH SPACE! Also the transaction logs of the TEMPDB will need a huge amount of free space. Also don&rsquo;t run this scripts during the day when you have several operators running the opsmgr console. My CPU went crazy to 100 % processor time so my advice is to run the query at night or during the weekend.

&nbsp;

&nbsp;

  * Reindex the DB

USE OperationsManager  
go  
SET ANSI_NULLS ON  
SET ANSI_PADDING ON  
SET ANSI_WARNINGS ON  
SET ARITHABORT ON  
SET CONCAT\_NULL\_YIELDS_NULL ON  
SET QUOTED_IDENTIFIER ON  
SET NUMERIC_ROUNDABORT OFF  
EXEC SP_MSForEachTable &#8220;Print &#8216;Reindexing &#8216;+&#8217;?&#8217; DBCC DBREINDEX (&#8216;?&#8217;)&#8221;

&nbsp;

&nbsp;

Now the results! 🙂

&nbsp;

Before running the script:

[<img height="244" width="215" src="http://scug.be/scom/files/2012/06/clip_image0024_thumb_1D5D6459.jpg" alt="clip_image002[4]" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image0024_3D787116.jpg)

After running the script:

[<img height="223" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_3626DA47.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_7A674193.png)

&nbsp;

Gain in diskspace:

OperationsManager free space in %:

&nbsp;

[<img height="140" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_5CF4F087.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_681E7AD1.png)

&nbsp;

OperationsManager free space in MB:

[<img height="139" width="244" src="http://scug.be/scom/files/2012/06/clip_image00210_thumb_11C7A71A.jpg" alt="clip_image002[10]" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image00210_1CF13164.jpg)

&nbsp;

&nbsp;

&nbsp;

&nbsp;

I was really suprised by the ammount of free space I had now. With cleaning up the localizetable I won about 60 % of space!

&nbsp;

My Opsmgr console is running really smootly now!

&nbsp;

Hope this helps,

Alexandre Verkinderen
