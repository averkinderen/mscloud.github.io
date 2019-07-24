---
id: 2211
title: 'Collect Processor time % of the HealthService.exe of your agents'
date: 2009-06-08T21:01:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2009/06/08/collect-processor-time-of-the-healthservice-exe-of-your-agents.aspx
permalink: /collect-processor-time-of-the-healthservice-exe-of-your-agents/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2110"
  - "2110"
  - "2110"
  - "2110"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Agent
  - Operations Manager 2007
  - Opmsgr 2007 R2
  - opsmgr
  - opsmgr R2
  - Performance
  - scom
---
If you have performance problems on your agents it&rsquo;s probably the healthservice.exe that&rsquo;s taking a lot of processor time %. At the moment only the processor time of the healthservice of the management servers is collected. This mean you will need to create a new collection performance rule to collect the processor time of the healthservice on your agents.

To have an overview of the processor time % of the healthservice.exe of all your agents follow the following procedure.

&nbsp;

Create a collection performance rule

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_7A8AE334.png" width="244" border="0" height="219" />](http://scug.be/scom/files/2012/06/image_2E9F8288.png)

Click next

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_1169B4B1.png" width="244" border="0" height="216" />](http://scug.be/scom/files/2012/06/image_0BFB440D.png)

Click next

&nbsp;

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_68126CB2.png" width="244" border="0" height="216" />](http://scug.be/scom/files/2012/06/image_70E274FE.png)

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_0E081D09.png" width="244" border="0" height="193" />](http://scug.be/scom/files/2012/06/image_75787FB8.png)

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_64B0D50A.png" width="244" border="0" height="215" />](http://scug.be/scom/files/2012/06/image_6D80DD56.png)

Click next

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_4FDEDC8A.png" width="244" border="0" height="218" />](http://scug.be/scom/files/2012/06/image_7216E810.png)

Select use optimization and click create.

&nbsp;

Now you can create a custom performance view to see the collected information:

&nbsp;

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_0DF7F73C.png" width="244" border="0" height="197" />](http://scug.be/scom/files/2012/06/image_3D29E2D3.png)

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_395C1836.png" width="244" border="0" height="159" />](http://scug.be/scom/files/2012/06/image_748FF401.png)

&nbsp;

This view shows you the processor time % of the healthservice.exe that&rsquo;s running on your agents.

&nbsp;

Hope this helps,

Alexandre Verkinderen