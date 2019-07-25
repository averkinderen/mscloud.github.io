---
id: 2891
title: 'The System Center Management service terminated with service-specific error %%-2147467259'
date: 2011-06-03T05:19:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2011/06/03/the-system-center-management-service-terminated-with-service-specific-error-2147467259.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "5982"
  - "5982"
  - "5982"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Agent
  - Agents
  - Issue
  - opsmgr
  - opsmgr R2
  - registry
---
I had the following issue on one of my servers 

“The System Center Management service terminated with service-specific error %%-2147467259” when I wanted to start my Healthservice.

[<img style="border-right-width: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_2AF3EDDD.png" width="244" height="97" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_20369688.png)

&#160;

When searching the internet I found the following blogpost [http://blogs.technet.com/b/smsandmom/archive/2008/04/30/opsmgr-2007-healthservice-service-fails-to-start-with-25362-warning.aspx](http://blogs.technet.com/b/smsandmom/archive/2008/04/30/opsmgr-2007-healthservice-service-fails-to-start-with-25362-warning.aspx "http://blogs.technet.com/b/smsandmom/archive/2008/04/30/opsmgr-2007-healthservice-service-fails-to-start-with-25362-warning.aspx")&#160; . The blogposts says that the State directory registry key can be corrupt but that was fine in my case.

But at the end of the blogpost I found my solution:

This error can be caused by the WindowsAccountLockDownSD Key in at HKEY\_LOCAL\_MACHINESYSTEMCurrentControlSetServicesHealthServiceParametersManagement Group<Management Group Name Here> being invalid or non-present.&#160; And indeed, that was my issue: the WindowsAccountLockDownSD Key was missing on my server.

&#160;

[<img style="border-right-width: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_0F6EEBDA.png" width="244" height="56" />](http://scug.be/scom/files/2012/06/image_313AC46B.png)

The easiest way to resolve the issue with the Windows AccountLockDownSD key is to export the registry key from a similar, working system and then import it in to the registry of the server experiencing the problem.&#160; Once this is complete the HealthService should start successfully.

[<img style="border-right-width: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_6617A3DB.png" width="244" height="47" />](http://scug.be/scom/files/2012/06/image_07E37C6D.png)

&#160;

thanks,

Alexandre Verkinderen
