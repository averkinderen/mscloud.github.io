---
id: 555
title: IIS 7 management pack hotfix
date: 2009-04-08T20:58:39+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2009/04/08/iis-7-management-pack-hotfix.aspx
permalink: /iis-7-management-pack-hotfix/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1572"
  - "1572"
  - "1572"
  - "1572"
  - "1572"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - IIS
  - Issue
  - Management Pack
  - Operations Manager 2007
  - opsmgr
  - opsmgr R2
  - Windows 2008
---
As mentioned on the MOM team blog there was a <a href="http://blogs.technet.com/momteam/archive/2009/02/25/problem-with-the-iis-modules-qfe-957123.aspx" target="_blank">problem with the IIS 7 Managemenent pack</a>. After importing the Windows Server 2008 Internet Information Services 7.0 management pack, the Health Service will log error 4507. The issue is in the setup code which causes the SDK and Configuration services on the RMS to be stopped and disabled.

&#160;

Today they released a <a href="http://www.microsoft.com/downloads/details.aspx?FamilyID=f82ef6b3-a08e-4295-b9e3-fb78a74aefa8&displaylang=en" target="_blank">hotfix that you can find here</a>.

&#160;

This hotfix impacts the following installed files:  
MomModules.dll (Version 06.0.6278.43)  
MomModules2.dll (Version 06.0.6278.43)  
MomIISModules.dll (Version 06.0.6278.43)  
MomModuleMsgs.dll (Version 06.0.6278.43)

&#160;

###### **<u>Important Notice</u>: A problem was found with this package, we are working on resolving it.**  
This hotfix must be applied to each computer that meets the following criteria: 

  * Hosts a Microsoft Operations Manager Root Management Server 
  * Hosts a Microsoft Operations Manager Management Server 
  * Hosts a Microsoft Operations Manager Gateway Server 
  * Host a Microsoft Operations Manually Installed Agent (Discover-based agent deployment not used) 

To extract the hotfix files contained in this hotfix:

  1. Copy the file, **SystemCenterOperationsManager2007-SP1-KB957123-X86-X64-IA64-ENU.MSI,** to either a local folder or accessible network shared folder. 
  2. Then run **SystemCenterOperationsManager2007-SP1-KB957123-X86-X64-IA64-ENU.MSI** locally on each applicable computer that meets the predefined criteria.  
    You can run **SystemCenterOperationsManager2007-SP1-KB957123-X86-X64-IA64-ENU.MSI** from either Windows Explorer or from a command prompt. 

**NOTE: To run this file on Windows Server 2008 you must run this file from a command prompt which was executed with the Run as Administrator option. Failure to execute this Windows installer file under an elevated command prompt will not allow display of the System Center Operations Manager 2007 Software Update splash screen to allow installation of the hotfix.**

&#160;

Grtz,

Alexandre verkinderen
