---
id: 2711
title: Cumulative Update 2 for OpsMgr 2007 R2 Connectors
date: 2010-07-31T07:38:07+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2010/07/31/cumulative-update-2-for-opsmgr-2007-r2-connectors.aspx
permalink: /cumulative-update-2-for-opsmgr-2007-r2-connectors-2/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2030"
  - "2030"
  - "2030"
  - "2030"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - connectors
  - Cumulative Update
  - Opmsgr 2007 R2
  - opsmgr
  - opsmgr R2
---
Microsoft just released Cumulative update 2 for the Systems Center Operations Manager 2007 R2 Connectors.

We now support:

  * **HP Operations Manager for UNIX v9** running on
  * HPUX 11i v3 Itanium 
  * Solaris 10 SPARC 
  * Red Hat Enterprise Linux 5.2 x64

  * **BMC Remedy AR System 7.5**

and some bug fixes as well:

  * Potential high CPU usage of HP OVO Event Consumer for Windows (scinteropd.exe)
  * Synchronization issue in HP OVO Connector
  * Remedy connectors do not populate the Computer Name and Domain fields
  * Unresponsiveness of the Interop provider when an Enterprise Management Service (EMS) API call returns an error
  * Incorrect dates are passed to the remote system by the connector
  * Product Knowledge is not forwarded when the locale is Canadian English

You can find more information or download the <a href="http://www.microsoft.com/downloads/details.aspx?FamilyID=87c27d91-4549-4169-a87a-ca88e4136e4f&displaylang=en" target="_blank">CU2 from here</a>.

&#160;

Hope this helps,

Alexandre Verkinderen