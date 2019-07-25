---
id: 647
title: System Center Advisor Changing the upload frequency
date: 2011-05-09T11:36:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2011/05/09/system-center-advisor-changing-the-upload-frequency.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2511"
  - "2511"
  - "2511"
  - "2511"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Advisor
  - age
  - Agent
  - Agents
  - c
  - Cloud
  - gateway
  - registry
  - system center
  - system center advisor
---
Most of the configuration like changing upload frequency is done in the registry.

The registry keys for the gateway are stored in HKEY\_LOCAL\_MACHINESoftwareMicrosoftSystemCenterAdvisorGateway and the registry keys for the agent are stored in HKLMSoftwareMicrosoftSystemCenterAdvisorAgent. If you change anything in the registry keys you will have to restart the **System Center Management** services on the agent and the **System Center Advisor Gateway** services on the gateway server**.**

****

[<img style="border-bottom: 0px;border-left: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top: 0px;border-right: 0px;padding-top: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_4EB7F998.png" width="244" height="191" />](http://scug.be/scom/files/2012/06/image_5068C56C.png)

By default the gateway only uploads once a day to the Advisor cloud services. Now for demo purposes I’m going to change it to every 12hours.

[<img style="border-bottom: 0px;border-left: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top: 0px;border-right: 0px;padding-top: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_13F050C2.png" width="244" height="217" />](http://scug.be/scom/files/2012/06/image_42B60964.png)

Have a look at the following site [http://onlinehelp.microsoft.com/en-us/advisor/ff962521.aspx](http://onlinehelp.microsoft.com/en-us/advisor/ff962521.aspx "http://onlinehelp.microsoft.com/en-us/advisor/ff962521.aspx") that describes all the registry keys.

&#160;

Thanks,

Alexandre Verkinderen
