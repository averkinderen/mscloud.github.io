---
id: 728
title: SCSM The report server cannot process the report or shared dataset
date: 2013-12-08T07:33:59+10:00
author: alexandre@verkinderen.com

guid: http://scug.be/scom/?p=728
sc_member_order:
  - "0"
post_views_count:
  - "2103"
  - "2103"
  - "2103"
  - "2103"
categories:
  - SystemCenter
tags:
  - reporting
  - reports
  - SCSM
  - sql
  - system center
---
&#160;

I encountered the following issue while trying to run a report from the Service Manager console: 

[<img title="scsm" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px 0px 15px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="scsm" src="http://www.mscloud.be/wp-content/uploads/2013/12/scsm_thumb.png" width="644" height="401" />](http://www.mscloud.be/wp-content/uploads/2013/12/scsm.png)

This was a total new installation (done by the Power Depoloyment Toolkit) and everything was installed fine without any errors so I doubled check my SQL, my datawarehouse server, my SQL reporting Service and by digging deeper and deeper into the reports themself on the SQL report I discovered the following error:

&#160;

[<img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.mscloud.be/wp-content/uploads/2013/12/image_thumb.png" width="644" height="387" />](http://www.mscloud.be/wp-content/uploads/2013/12/image1.png)

So that was the culprit!&#160; To solve this issue, open the configuration of each report, go to data sources and select the DWDataMart Data source:

[<img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; margin: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.mscloud.be/wp-content/uploads/2013/12/image_thumb11.png" width="244" height="128" />](http://www.mscloud.be/wp-content/uploads/2013/12/image11.png)

&#160;

click OK and now you will be able to run reports again! 

&#160;

Thanks,

Alexandre Verkinderen
