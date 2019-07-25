---
id: 2161
title: Opsmgr DB Create wizard System.InvalidOperationException
date: 2009-05-29T19:19:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2009/05/29/opsmgr-db-create-wizard-system-invalidoperationexception.aspx
permalink: /opsmgr-db-create-wizard-system-invalidoperationexception-2/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2111"
  - "2111"
  - "2111"
  - "2111"
  - "2111"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Database
  - Issue
  - manuals
  - Operations Manager 2007
  - Opsmgr DB
  - opsmgr R2
  - scom
  - sql
---
Today I wanted to install my OperationsmanagerDB on my SQL cluster 2005 SP2 actif-passive.

So I started the DBCreatewizard.exe and I got a very strange error mentioning something about

&nbsp;

Severity: Error Message: Database creation failed. The database might have been incompletly created or modified. System.InvalidOperationException: An error occurred while trying to create the database on your SQL Server. Check your logs for more information. at Microsoft.EnterpriseManagement.Setup.DBCreateWizard.Program.LaunchDBCreation() at Microsoft.EnterpriseManagement.Setup.DBCreateWizard.SummaryPage.BackgroundThread()

&nbsp;

[<img height="194" width="244" src="http://scug.be/scom/files/2012/06/clip_image002_thumb_3815DCC1.jpg" alt="clip_image002" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image002_618A1E01.jpg)

&nbsp;

To make a long story short:

We had a lab environment and production environment. Both environments are exact replicas: ip, users, servers, everything is the same. I did the install in the lab environment on my sql cluster and didn&rsquo;t encounter any problems.

Now in production I had this strange error and asked my dba (that installed the sql cluster in lab and production) to confirm that everything was ok and that everything was the exact replica of the lab&hellip;.

Now here comes the catch&hellip;.and also the moment I wanted to kill my DBA&hellip;.

I analyzed the dbcreatewizard error log that you can find here:

&nbsp;

C:Documents and SettingsuserLocal SettingsTemp1

[<img height="184" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_503BD7CD.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_57C4B689.png)

And found the following sentence

&nbsp;

10:31: CreateDB:&nbsp; Attempting to create OperationsManager on ELSQL3EWSSCOM threw the following sql exception Cannot use file &#8216;J:SCOMOPLOGOperationsManager.ldf&#8217; for clustered server. Only formatted files on which the cluster resource of the server has a dependency can be used. **Either the disk resource containing the file is not present in the cluster group or the cluster resource of the Sql Server does not have a dependency on it.**

&nbsp;

[<img height="196" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_6F83A002.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_0065B342.png)

I checked on my cluster resource and indeed: the Log disk was missing as a dependency!!

[<img height="209" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_59BC4856.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_3CB3998E.png)

So my production environment was not the exact replica as my lab environment. I had to add the Log file disk as a dependency for my sql resource group:

[<img height="244" width="233" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_49B00A50.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_2E0B7E5A.png)

&nbsp;

And now I was able to run the dbcreatewizard.exe succesfully!

&nbsp;

[<img height="215" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_4DBCE8D3.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_251E7CCC.png)

&nbsp;

Hope this helps,

Alexandre Verkinderen
