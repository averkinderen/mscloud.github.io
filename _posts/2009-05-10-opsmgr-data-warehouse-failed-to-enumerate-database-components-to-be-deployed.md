---
id: 560
title: Opsmgr Data Warehouse failed to enumerate database components to be deployed
date: 2009-05-10T09:04:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2009/05/10/opsmgr-data-warehouse-failed-to-enumerate-database-components-to-be-deployed.aspx
permalink: /opsmgr-data-warehouse-failed-to-enumerate-database-components-to-be-deployed/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2487"
  - "2487"
  - "2487"
  - "2487"
  - "2487"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - hotfix
  - Issue
  - KB
  - Management Pack
  - manuals
  - Operations Manager 2007
  - opsmgr
  - reporting
  - scom
  - sql
---
Today I ran into this issue:

[<img height="244" width="221" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_760054DE.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_5D6E26DD.png)

&nbsp;

Data Warehouse failed to enumerate database components to be deployed. Failed to enumerate Data Warehouse components for deployment. The operation will be retried. Exception &#8216;SqlException&#8217;: Timeout expired. The timeout period elapsed prior to completion of the operation or the server is not responding. One or more workflows were affected by this. Workflow name: Microsoft.SystemCenter.DataWarehouse.Deployment.Component Instance name: scom.be Instance ID: {AC6FACD9-

&nbsp;

**Issue**:This error appears immediately after a management pack is imported. The installaion of the reports in the MP is failing.

**Resolution**:Run **exec sp_updatestats** on the OperationsManagerDW db (the data warehouse).

&nbsp;

When running the exec sp_updatestats doesn&rsquo;t help follow these steps:

&nbsp;

Download and extract the following hotfix:

&nbsp;

[http://support.microsoft.com/?kbid=954643](http://support.microsoft.com/?kbid=954643 "http://support.microsoft.com/?kbid=954643")

[<img height="77" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_1A28401F.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_1138ADE0.png)

&nbsp;

Run the SQL query Managementpackinstall.sp.sql

[<img height="172" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_0226F068.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_39D719E7.png)

&nbsp;

And directly after running the query I got the following event:

[<img height="244" width="221" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_4D1CF1E8.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_0F8D036E.png)

&nbsp;

Everything is fine now and I have green management server:

&nbsp;

[<img height="143" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_1A4CEB74.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_33B4EEAE.png)

&nbsp;

Hope this help,

Alexandre Verkinderen

[http://scug.be](http://scug.be/)
