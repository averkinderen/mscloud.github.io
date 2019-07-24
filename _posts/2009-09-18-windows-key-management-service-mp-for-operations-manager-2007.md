---
id: 590
title: Windows Key Management Service MP for Operations Manager 2007
date: 2009-09-18T17:53:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2009/09/18/windows-key-management-service-mp-for-operations-manager-2007.aspx
permalink: /windows-key-management-service-mp-for-operations-manager-2007/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1924"
  - "1924"
  - "1924"
  - "1924"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Database
  - Issue
  - KMS
  - Management Pack
  - Operations Manager 2007
  - Opmsgr 2007 R2
  - opsmgr
  - Opsmgr DB
  - opsmgr R2
  - scom
  - Windows 2008
---
Microsoft just released a new KMS mp for opmsgr 2007. Be carefull when importing it via the catalog with the OpsMgr 2007 R2 console. Before importing the mp [<img style="border-right: 0px;border-top: 0px;margin-left: 0px;border-left: 0px;margin-right: 0px;border-bottom: 0px" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_1AD6E017.png" width="117" align="right" border="0" height="103" />](http://scug.be/scom/files/2012/06/image_6FFE7C04.png)you will need to uninstall any previous version of the mp AND you will also need to run a sql Clean up query to delete the previous KMS tables, KMS grooming jobs and any other KMS mp related stored procedure! This SQL cleanup query is not available when importing the management pack with the console. You will need to download and install the KMS mp from here: [http://www.microsoft.com/downloads/details.aspx?FamilyId=A330D876-C965-4433-AFDF-7C61A9126FB3&displaylang=en&displaylang=en](http://www.microsoft.com/downloads/details.aspx?FamilyId=A330D876-C965-4433-AFDF-7C61A9126FB3&displaylang=en&displaylang=en "http://www.microsoft.com/downloads/details.aspx?FamilyId=A330D876-C965-4433-AFDF-7C61A9126FB3&displaylang=en&displaylang=en")

&nbsp;

<a name="_Toc240443590">Changes in This Update</a><a name="z15189026c30248e59c67571a87444bd6"></a>

The 6.0.7234.0 version of the KMS Management Pack includes the following changes:

&middot; Support for Windows 7 and Server 2008 R2

&middot; Decommissioning of KMS reports

&middot; Support for non-Windows KMS applications

&middot; Installation / un-installation changes

<a name="_Toc240443591">Supported Configurations</a><a name="z050b32cc968b4c5d9ae0d49ec8252be5"></a>

This management pack supports up to twenty KMS hosts. The following table details the supported configurations for the KMS Management Pack

<table border="1" cellpadding="0" cellspacing="0">
  <tr>
    <td valign="top" width="294">
      <b>Configuration</b>
    </td>
    
    <td valign="top" width="293">
      <b>Support</b>
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="294">
      Windows Server 2008 R2
    </td>
    
    <td valign="top" width="293">
      Yes, all editions, 32-bit and 64-bit
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="294">
      Windows Server 2008
    </td>
    
    <td valign="top" width="293">
      Yes, all editions, 32-bit and 64-bit
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="294">
      Agentless monitoring
    </td>
    
    <td valign="top" width="293">
      Not supported
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="294">
      Windows 7
    </td>
    
    <td valign="top" width="293">
      All volume editions
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="294">
      Windows Vista
    </td>
    
    <td valign="top" width="293">
      All volume editions
    </td>
  </tr>
</table>

&nbsp;

Before you import the Key Management Service Management Pack, take the following actions:

&middot; Remove any previous versions of the management pack at or below build # 6.0.6278.9

&middot; If the previous version of the management pack utilized reports, follow these steps:

  1. Open SQL Query Analyzer and select the OperationsManagerDW
  2. From SQL Query analyzer, open the Uninstall.sql.txt (rename to uninstall.sql if desired) file attached with this management pack
  3. Execute (F5)