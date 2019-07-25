---
id: 609
title: OpsMgr 2007 R2 Cumulative Update 1
date: 2010-01-18T07:13:23+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2010/01/18/opsmgr-2007-r2-cumulative-update-1.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1677"
  - "1677"
  - "1677"
  - "1677"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Cumulative Update
  - hotfix
  - Issue
  - opsmgr
  - opsmgr R2
---
Our first [cumulative update has released](http://www.microsoft.com/downloads/details.aspx?FamilyID=05d30779-2ddc-48dc-aa91-a23167ee2cad&displaylang=en) for OpsMgr 2007 R2! Cumulative Update 1 contains a number of fixes for the Operations Manager 2007 R2 release. More information about what has been fixed can be found here: [http://support.microsoft.com/kb/974144](http://support.microsoft.com/kb/974144 "http://support.microsoft.com/kb/974144") .

&#160;

And as always RTFM! You will need to perform some additional steps:

  * Update the DiscoveryEntitySPRocs.sql
  * and import the Microsoft.SystemCenter.DatawareHouse.Report.Library.mp manually

&#160;

Also notice that the issue with the SRSUpgradetool.exe, [as described here](http://thoughtsonopsmgr.blogspot.com/2009/08/r2-error-with-srsupgradetoolexe.html), has been resolved now:

The following updated file that is located in the **SupportTools** folder supports the upgrade from SQL Reporting Services 2005 to SQL Reporting Services 2008:**</p> 

SRSUpgradeTool.exe

    <p></p>   <b>Note</b> Use the appropriate platform version of this file instead of the file that is supplied in the <strong>SupportTools</strong> folder of the Operations Manager 2008 R2 distribution media.</b>  <p>&#160;</p>  <p>Hope this helps,</p>  <p>Alexandre Verkinderen
