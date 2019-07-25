---
id: 638
title: Installing a remote Operations Manager database with DBcreateWizard.exe
date: 2011-01-19T11:56:05+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2011/01/19/installing-a-remote-operations-manager-database-with-dbcreatewizard-exe.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1974"
  - "1974"
  - "1974"
  - "1974"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - dbcreatewizard
  - install
  - opsmgr
  - Opsmgr DB
  - opsmgr R2
  - R2
  - setup
---
Hi all,

One of my customers was asking me if he could install the OpsMgr database remotely. This is perfectly possible with DBCreatewizard tool. The DBcreatewizard tool is a small tool that let you install the Opsmgr database and the datawarehouse without running the setupOM.exe wizard. Kevin Holman has <a href="http://blogs.technet.com/b/kevinholman/archive/2008/05/03/dbcreatewizard-or-just-run-good-old-setupom-exe-which-should-i-use-to-install-the-database-component-of-opsmgr.aspx" target="_blank">blogpost</a> on whether you should use the DBcreatewizard or just the good old setupOM.exe

&#160;

By running the following command you can install the OperationsManager DB locally or remotely by specifying the severname:

DBCreateWizard.exe DBType:"Operations Manager Database" SQLInstance:OpsMgrSQserverLinfrontscomInstance DBName:OperationsManager ManagementGroup:OperationsManager UserGroup:InfrontscomOpsMgrAdmins AutoErrorReport DBCreate DBSize:5000 DBPath:"C:Program FilesMicrosoft SQL ServerMSSQL10.INFRONTSCOMDATA" LOGPath:"C:Program FilesMicrosoft SQL ServerMSSQL10.INFRONTSCOMMSSQLLog"

&#160;

&#160;[<img style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_640113C4.png" width="215" height="23" />](http://scug.be/scom/files/2012/06/image_04F4866C.png) 

&#160;

And for the Datawarehouse run the following command:

DBCreateWizard.exe DBType:"Operations Manager Data Warehouse Database" SQLInstance:OpsMgrSQLserverinfrontscomInstance DBName:OperationsManagerDW AutoErrorReport DBCreate DBSize:500 DBPath:"C:Program FilesMicrosoft SQL ServerMSSQL10\_50.MSSQLSERVERMSSQLDATA" LOGPath:"C:Program FilesMicrosoft SQL ServerMSSQL10\_50.MSSQLSERVERMSSQLLog"

&#160;

In your local user temp folder C:Documents and SettingsuserLocal SettingsTemp1&#160; you will find a log file each time you run the dbcreatewizard tool.

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;  
Starting Logging for Setup.exe 13:19:14 dinsdag 4 januari 2011  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;  
13:19: GetlocalSQLServerPath: caught an exception: Invalid namespace  
13:19: GetlocalSQLServerPath: caught an exception: Invalid namespace  
13:19: GetlocalSQLServerPath: caught an exception: Invalid namespace  
13:19: GetlocalSQLServerPath: caught an exception: Invalid namespace  
13:19: Creating database&#8230;  
13:21: **Database created successfully.  
** &#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;  
Finished Logging for Setup.exe 13:21:19 dinsdag 4 januari 2011  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;
