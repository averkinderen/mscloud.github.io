---
id: 2291
title: Known issues with the Microsoft Dynamics AX 2009 Management Pack for Systems Center Operations Manager 2007
date: 2009-06-23T21:03:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2009/06/23/known-issues-with-the-microsoft-dynamics-ax-2009-management-pack-for-systems-center-operations-manager-2007.aspx
permalink: /known-issues-with-the-microsoft-dynamics-ax-2009-management-pack-for-systems-center-operations-manager-2007-2/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1689"
  - "1689"
  - "1689"
  - "1689"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Axapta
  - dynamics
  - Issue
  - Management Pack
  - Operations Manager 2007
  - Opmsgr 2007 R2
  - opsmgr
  - opsmgr R2
---
Microsoft just published a <a target="_blank" href="http://blogs.technet.com/operationsmgr/archive/2009/06/23/known-issues-with-the-microsoft-dynamics-ax-2009-management-pack-for-systems-center-operations-manager-2007.aspx">known issue with</a> the Microsoft Dynamics AX 2009 Management Pack for Systems Center Operations Manager 2007.

&nbsp;

We&rsquo;ve seen a couple issues with the Microsoft Dynamics AX 2009 Management Pack for Systems Center Operations Manager 2007 that we just released and found that the issues did not impact the operation of the management pack but were generating some non-actionable alerts. As a result, we wanted to make everyone aware of these so they wouldn&rsquo;t cause any undue concern.

The following are some of the known issues in the Dynamics AX 2009 Management pack.

**<span style="text-decoration: underline">Issue :</span>** Alert &ldquo;A GroupPopulator module unloaded due to an unrecoverable error&rdquo; in operations manager console when importing the Dynamics AX 2009 Management Pack

Affected Version : 1.0.0.50

Description : This error is generated due to a race condition on the RMS where a group populator gets fired before the management pack gets loaded completely. This does not impact the performance or functionality of the management pack.

Resolution : There is no resolution for this problem since it&rsquo;s due to a race condition. Just close the alert.

**<span style="text-decoration: underline">Issue :</span>** Alert &ldquo;Script or Executable Failed to run&rdquo; in operations manager console

Affected Version : 1.0.0.50

Description : Some placeholder scripts (myscript.vbs) in the Dynamics AX 2009 Management Pack cause SCOM to generate warnings because there is no code being executed.

Resolution : There is no resolution for this alert. Close the alert. The problem will be fixed in the next version of the management pack.

**Raji Easwaran | Senior Program Manager**

****

**Here is a screenshot of the alert of the group populated error:**

[<img height="183" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_1141EE29.png" alt="image" border="0" style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" />](http://scug.be/scom/files/2012/06/image_3F7BE9E3.png)

**Here is a screenshot of the empty scripts:**

[<img height="183" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_3924ED88.png" alt="image" border="0" style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" />](http://scug.be/scom/files/2012/06/image_776DB7F9.png)

I want to thank Raji Easwaran for helping me with these issues.&nbsp;She was really helpfull and always available! Thank you Raji!

&nbsp;

Alexandre Verkinderen