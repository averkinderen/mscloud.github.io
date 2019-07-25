---
id: 19683
title: Opsmgr Service Level Dashboard for Exchange 2007
date: 2009-01-23T14:31:09+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2009/01/23/opsmgr-service-level-dashboard-for-exchange-2007.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1770"
  - "1770"
  - "1770"
  - "1770"
  - "1770"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Issue
  - Operations Manager 2007
  - opsmgr
  - scom
  - service level dashboard
---
It is possible to create custom reports for Exchange 2007 using the Service Level Dashboard Solution Accelerator and the Exchange 2007 Management Pack. The Opsmgr Team made a <a href="http://blogs.technet.com/momteam/archive/2008/10/23/creating-exchange-2007-availability-reports-using-the-service-level-dashboard-solution-accelerator-and-the-exchange-2007-management-pack.aspx" target="_blank">nice guide</a> on how to make a Service Level Dashboard for Exchange.

&nbsp;

But you have to change the Monitor dependency of the distributed applications otherwise the Health wouldn&#8217;t rolling up.

&nbsp;

1. In the monitoring section of the console, under “Distributed Applications”, right-click on the “Exchange 2007 Server Availability” distributed application that you defined and select to open the Diagram View

2. Right-click on Exchange 2007 CAS Servers and select “Health Explorer”.

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="194" alt="sshot-1 (2)" src="http://scug.be/scom/files/2012/06/sshot-1-_2800_2_29005F00_thumb.png" width="244" border="0" />](http://scug.be/scom/files/2012/06/sshot-1-_2800_2_29005F00_2.png)

3. Right-click on Component Group Health Roll-up for type Ex. Client Access Servers and select “Monitor Properties”.

4. On the Monitor Dependency tab, click “**<u>MOM 2005 Computer Role Health</u>**” and click ok. This will allow health to roll up to the Component Group level. By default, health of converted Management Packs rolls up via MOM 2005 Computer Role Health.

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="244" alt="sshot-1 (3)" src="http://scug.be/scom/files/2012/06/sshot-1-_2800_3_29005F00_thumb.png" width="229" border="0" />](http://scug.be/scom/files/2012/06/sshot-1-_2800_3_29005F00_2.png)

&nbsp;

But now come the tricky part. The state of you distributed applications will stay on unmonitored until a state change occurred for state to start rolling up.

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="217" alt="sshot-1 (4)" src="http://scug.be/scom/files/2012/06/sshot-1-_2800_4_29005F00_thumb.png" width="244" border="0" />](http://scug.be/scom/files/2012/06/sshot-1-_2800_4_29005F00_2.png)

&nbsp;

The solution for this problem is just to put your exchange servers in maintenance mode for a while!

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="158" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb.png" width="244" border="0" />](http://scug.be/scom/files/2012/06/image_2.png)

&nbsp;

That&#8217;s how I resolved the unmonitored issue for my service level dashboard.

&nbsp;

Grtz,

Alexandre Verkinderen

&nbsp;

After the maintenance mode my
