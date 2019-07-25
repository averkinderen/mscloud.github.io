---
id: 19676
title: Changing the ACS DataRetention Period for Opsmgr
date: 2008-09-19T13:23:04+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2008/09/19/changing-the-acs-dataretention-period-for-opsmgr.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2934"
  - "2934"
  - "2934"
  - "2934"
  - "2934"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - acs
  - audit collection service
  - Operations Manager 2007
  - opsmgr
  - scom
---
**Changing the Audit Collection Service DataRetention Period** (based on the info found on the technet site)

Operations Manager grooms, or removes, data from its various databases at regular configurable intervals. For the Operations database, this is done in the Operations console. For the ACS database, these settings are configured during setup with a default value of 14 days. This means that every day, all database partitions (and their data) that are older than 14 days are dropped or deleted. Because of the volume of data that ACS can accumulate, 14 days is not an unreasonable setting. However, some companies might need to retain data for longer periods and they must have already planned for that when making the sizing and performance calculations for their environment. You can change the retention period for the ACS data by following this procedure.

To Change the ACS Data- Retention Period

1. Log on to the computer running SQL Server that hosts the ACS database with an account that has administrative rights to the ACS database.

2. Open the SQL Server Management Studio tool, and connect to the database engine.

3. Expand the **Databases** folder, and select the **OperationsManagerAC** database.

4. Right-click to open the context menu and select **New Query…**.

5. Run the following query to see what your retention period is: **SELECT * FROM dtConfig**

**[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="215" alt="clip_image002" src="http://scug.be/blogs/scom/WindowsLiveWriter/ChangingtheACSDataRetentionPeriodforOpsm_D8B2/clip_image002_thumb.jpg" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/ChangingtheACSDataRetentionPeriodforOpsm_D8B2/clip_image002_2.jpg)**

Look for row 6. The result contains the days to retain + 1

6. In the Query pane, type the following, where **number of days to retain data + 1** equals the number of days you want to pass before data that has aged past that point is deleted. For example, if you want to retain data for 30 days, type **31**

**USE OperationsManagerAC UPDATE dtConfig SET Value = <number of days to retain data + 1> WHERE Id = 6** and then click the **Execute** button on the toolbar. This will run the query and then open the **Messages** pane, which should read **(1 row(s) affected).**

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="105" alt="clip_image004" src="http://scug.be/blogs/scom/WindowsLiveWriter/ChangingtheACSDataRetentionPeriodforOpsm_D8B2/clip_image004_thumb.jpg" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/ChangingtheACSDataRetentionPeriodforOpsm_D8B2/clip_image004_2.jpg)

7. To view the new setting, delete the previous query text from the Query pane and enter **SELECT * FROM dtConfig**. This will open the **Results** pane below the Query pane.

8. Look at the value in the sixth row; it should now equal the value you entered for <number of days to retain data + 1>.

9. Restart the **Operations Manager Audit Collection Service** for this to take effect.

&nbsp;

Greetz,

Alkin

<http://scug.be/blogs>

&nbsp;

<div class="wlWriterSmartContent" style="padding-right: 0px;padding-left: 0px;padding-bottom: 0px;margin: 0px;padding-top: 0px">
  Tags van Technorati: <a href="http://technorati.com/tags/opsmgr" rel="tag">opsmgr</a>,<a href="http://technorati.com/tags/acs" rel="tag">acs</a>,<a href="http://technorati.com/tags/scom" rel="tag">scom</a>,<a href="http://technorati.com/tags/audit%20collection%20service" rel="tag">audit collection service</a>
</div>
