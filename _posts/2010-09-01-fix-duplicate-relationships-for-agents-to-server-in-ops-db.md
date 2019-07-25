---
id: 633
title: Fix duplicate relationships for agents to server in Ops DB
date: 2010-09-01T09:34:41+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2010/09/01/fix-duplicate-relationships-for-agents-to-server-in-ops-db.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2407"
  - "2407"
  - "2407"
  - "2407"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Agent
  - Agents
  - Database
  - Issue
  - KB
  - Opmsgr 2007 R2
  - opsmgr
  - opsmgr R2
---
Sometimes it can happen that agents are ending up with multiple primary management server relationships. Of course you can only have one primary server relationship! In the rare occasions that you end up with multiple primary relationships you can now repair the issue by running the new _“Fix duplicate relationships for agents to server in Ops DB”_ task manually

[<img style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_3894D406.png" width="644" height="246" />](http://scug.be/scom/files/2012/06/image_325E2345.png) 

or there is a recovery on this monitor (disabled by default) that you can turn on so that the issue will be fixed automatically:

[<img style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_2B8ACE28.png" width="644" height="311" />](http://scug.be/scom/files/2012/06/image_345AD674.png) 

[<img style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_7F9A2E9E.png" width="244" height="113" />](http://scug.be/scom/files/2012/06/image_4114E0F8.png) 

&#160;

You will need the latest OpsMgr 2007 R2 management pack that you can find here [http://www.microsoft.com/downloads/details.aspx?FamilyID=61365290-3c38-4004-b717-e90bb0f6c148&displaylang=en](http://www.microsoft.com/downloads/details.aspx?FamilyID=61365290-3c38-4004-b717-e90bb0f6c148&displaylang=en "http://www.microsoft.com/downloads/details.aspx?FamilyID=61365290-3c38-4004-b717-e90bb0f6c148&displaylang=en")

Thanks,  
Alexandre Verkinderen
