---
id: 2261
title: Microsoft Exchange Server 2007 Management Pack for System Center Operations Manager 2007 R2
date: 2009-06-13T07:45:20+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2009/06/13/microsoft-exchange-server-2007-management-pack-for-system-center-operations-manager-2007-r2.aspx
permalink: /microsoft-exchange-server-2007-management-pack-for-system-center-operations-manager-2007-r2-2/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1552"
  - "1552"
  - "1552"
  - "1552"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Exchange
  - Management Pack
  - Opmsgr 2007 R2
  - opsmgr R2
  - scom
---
The new Exchange Server 2007 management pack for Opsmgr 2007 R2 is now RTM and available from the <a href="http://www.microsoft.com/downloads/details.aspx?FamilyID=e9f3cd3f-9bc0-45cd-b10f-120e937ee4c4&amp;displaylang=en&displaylang=en" target="_blank">mp catalog</a>!

New monitoring wizard for configuring the Exchange MP:

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="214" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_4EDE0725.png" width="244" border="0" />](http://scug.be/scom/files/2012/06/image_170BC302.png) 

&#160;

&#160;

**Feature Summary**

  * A number of synthetic transactions ensure the Exchange servers are available and responding in a timely manner. The synthetic transactions are maintenance-mode aware, so that if the target of a transaction is in maintenance mode, the source will not run the transaction, and not alert unnecessarily. 
  * This Management Pack includes a Management Pack template that provides a wizard-like interface for configuring synthetic transactions against Outlook Web Access (OWA), Exchange ActiveSync, Web Services, POP3, and IMAP. 
  * This Management Pack includes a Management Pack template that provides a wizard-like interface for configuring mail flow synthetic transactions between agent-managed Exchange 2007 Mailbox servers. 
  * This Management Pack provides 30+ reports specific to Exchange 2007 that track availability and performance compared to service level objectives. For the list of reports and for more information about the reports, see the Management Pack Guide. 
  * All the synthetic transactions in this Management Pack use an Operations Manager 2007 R2 hosting feature for Windows PowerShell technology that provides a performance improvement when running synthetic transactions. 
  * A significant number of rules and monitors that are not actionable or may be noisy are disabled. Note that many of these rules are still in the Management Pack so that you can enable them if necessary. 
  * Support for monitoring any number of Exchange organizations using a single Operations Manager 2007 management group. 
  * Full support for Microsoft clustered configurations. For more details, see the Management Pack Guide. 
  * Discovery of Exchange 2007 server roles is disabled by default, and no Exchange 2007 monitoring is applied by default. This allows you to discover and monitor your servers gradually, as well as tune the Management Pack as you bring more agent-managed Exchange 2007 servers into the Operations Manager environment. 

&#160;

&#160;

Grtz,

Alexandre Verkinderen