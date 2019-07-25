---
id: 1871
title: The SQL Server Service Broker for the current Opsmgr database is not enabled
date: 2008-11-22T15:04:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2008/11/22/the-sql-server-service-broker-for-the-current-opsmgr-database-is-not-enabled.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1864"
  - "1864"
  - "1864"
  - "1864"
  - "1864"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Issue
  - Operations Manager 2007
  - opsmgr
  - scom
  - sql
---
Yesterday I came accros this error:

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="191" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_721930C0.png" width="244" border="0" />](http://scug.be/scom/files/2012/06/image_6E5B8BF0.png) 

Saying that the SQL server Service Broker or database mirroring endpoint is disabled or not configured.

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="244" alt="clip_image002[4]" src="http://scug.be/scom/files/2012/06/clip_image002[4_5D005F00_thumb_6F23CC0D.jpg" width="222" border="0" />](http://scug.be/scom/files/2012/06/clip_image002[4_5D005F00_7C6A5520.jpg)

If you don’t know what the SQL server service broker exactly is, have a look here: [An introduction to SQL server service broker](http://msdn.microsoft.com/en-us/library/ms345108.aspx). In summary the Service Broker, internal or external processes can send and receive guaranteed, asynchronous messaging by using extensions to Transact-SQL. And it needs to be up and running for our Opsmgr DB.

So I did a search on google and found [this post](http://blogs.technet.com/smsandmom/archive/2007/10/11/scom2007-moving-the-operations-manager-database.aspx) where they describe how to enable the service broker.

&#160;

In summary:

  1. First stop the opsmgr SDK service
  2. Open SQL Server Management Studio. 
  1. Click New Query
  1. In the query window, enter the following query: ALTER DATABASE OperationsManager SET SINGLE_USER WITH ROLLBACK IMMEDIATE
  2. Click Execute.

  2. Click New Query
  1. Enter the following query: ALTER DATABASE OperationsManager SET ENABLE_BROKER
  2. Click Execute.
  3. [<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="189" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_37363C25.png" width="244" border="0" />](http://scug.be/scom/files/2012/06/image_330C6460.png) 

  3. Click New Query.
  1. In the query window, enter the following query: ALTER DATABASE OperationsManager SET MULTI_USER
  2. Click Execute.
  3. [<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="215" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_46F5D129.png" width="244" border="0" />](http://scug.be/scom/files/2012/06/image_3AD45702.png) 

  3. You can verify the setting for ENABLE\_BROKER is set to 1 by using this SQL query: SELECT is\_broker_enabled FROM sys.databases WHERE name=&#8217;OperationsManager&#8217;. 
  4. Restart your Opsmgr SDK service.

&#160;

That’s it! 

&#160;

Grtz,

Alexandre Verkinderen

<http://scug.be/blogs>

&#160;

&#160;

&#160;
