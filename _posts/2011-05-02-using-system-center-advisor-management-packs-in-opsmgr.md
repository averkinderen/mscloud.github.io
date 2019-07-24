---
id: 645
title: Using System Center Advisor Management Packs in OpsMgr
date: 2011-05-02T06:59:35+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2011/05/02/using-system-center-advisor-management-packs-in-opsmgr.aspx
permalink: /using-system-center-advisor-management-packs-in-opsmgr/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2145"
  - "2145"
  - "2145"
  - "2145"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Advisor
  - Cloud
  - Management Pack
  - Operations Manager 2007
  - Operations Manager 2012
  - opsmgr
  - opsmgr 2012
  - opsmgr R2
  - system center
  - system center advisor
---
System Center Advisor has some extra management packs that are not available for OpsMgr.

The full list of data points collected by the agent is available for download [here](http://go.microsoft.com/fwlink/?LinkId=215200), from the Microsoft Download Center, in an Excel spreadsheet.&#160; For example, included in this list are properties about SQL Server like data from SERVERPROPERTY, sys.databases, and sys.configurations.

I think it’s a shame we don’t have those extra rules and monitors in the OpsMgr MP’s so I wanted to have those extra checks in my OpsMgr environment by importing the Advisor management packs! Let’s see if this will work!

You can find all Advisor management packs on the gateway in C:Program FilesSystem Center AdvisorGatewayDataContent 

&#160;

[<img style="border-right-width: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="SNAG_Program-0272" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0272_thumb_4CC1308C.png" width="244" height="160" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0272_58869D8B.png)

Just copy those Advisor MP’s to your Opsmgr box and import them:

[<img style="border-right-width: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="SNAG_Program-0273" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0273_thumb_68A23FB7.png" width="244" height="148" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0273_60DA4D15.png)

Once imported you will all those extra checks in your OpsMgr environment.

[<img style="border-right-width: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_7312EE0A.png" width="244" height="159" />](http://scug.be/scom/files/2012/06/image_154AF991.png)

And alerts are starting coming in that you didn’t get before:

[<img style="border-right-width: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_1BCE5354.png" width="244" height="189" />](http://scug.be/scom/files/2012/06/image_4B003EEB.png)

Thanks,

Alexandre Verkinderen