---
id: 643
title: System Center Advisor Part 1 Overview
date: 2011-04-30T09:25:19+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2011/04/30/system-center-advisor-part-1-overview.aspx
permalink: /system-center-advisor-part-1-overview/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1701"
  - "1701"
  - "1701"
  - "1701"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Advisor
  - Cloud
  - system center
---
Hi All,

I’m going to start posting a series of blogposts regarding System Center Advisor (formerly project Atlanta).&#160; System Center Advisor is a new cloud based offering of Microsoft that will monitor your environment (at this point only Windows Server and SQL server). Advisor will be the connection between your servers and Microsoft support services.

&#160;

It’s very important to know that Advisor is <font>not a REAL TIME MONITORING solution!!</font><font>&#160;&#160;&#160;&#160; You don’ t have:</font>

  * <font>real time monitoring</font> 
  * Real time alerting 
  * real time notification 
  * Reporting 
  * Monitoring of LOB 
  * ETC 

<font></font>

<font>Once a day the alerts will be send from the gateway to the Cloud service where you will be able to analyze it with the webconsole.</font>

&#160;

## Architecture:

When we look at the architecture of Advisor we have gateways and Agents. In your datacenter you will have to install an Advisor gateway that will upload once a day the collected data to the cloud, on your servers you want to monitor you need to install agents that will communicate with the gateway on port 80. By default each agent uploads CAB files to the gateway twice per day. The size of the CAB files depends on the configuration of the machine (such as number of SQL engines and number databases) and the health of the machine (e.g. the number of alerts generated). In most cases, the daily upload size is typically less than 100 KB.

&#160;

Advisor leverages Operations Manager 2007 R2 Agent and Management Pack technology and can run side by side with OpsMgr. When you install an Advisor agent on a computer that has a System Center Operations Manager 2007 R2 agent installed, the Health Service will be configured to run in multi-homing mode so that existing Operations Manager management groups are not impacted.

&#160;

Once the data has been uploaded, the Advisor cloud service will analyze the data and make it visible in the Advisor webconsole to you and to Microsoft CSS. The collected data is uploaded and archived on-premise for 5 days by default.

[<img style="border-right-width: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_3F985B6D.png" width="244" height="147" />](http://scug.be/scom/files/2012/06/image_18020510.png)

&#160;

Rules and monitors are finetuned and updated by Microsoft and periodically downloaded to the gateway.

## 

## RoadMap and Licensing

System Center Advisor will be free as a benefit for customer who has Software assurance.

[<img style="border-right-width: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_0102E7FA.png" width="244" height="136" />](http://scug.be/scom/files/2012/06/image_3015499E.png)

&#160;

In the next post I’m going to describe the installation process of System Center Advisor.

&#160;

Thanks,

Alexandre Verkinderen
