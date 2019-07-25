---
id: 19687
title: Upgrading Opsmgr 2007 R2 RC consoles to Opsmgr 2007 R2 RTM
date: 2009-05-26T19:37:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2009/05/26/upgrading-opsmgr-2007-r2-rc-consoles-to-opsmgr-2007-r2-rtm.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1462"
  - "1462"
  - "1462"
  - "1462"
  - "1462"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Consoles
  - Operations Manager 2007
  - Opmsgr 2007 R2
  - Opmsgr 2007 R2 RC
  - opsmgr R2
  - upgrade
---
When you want to start upgrading your consoles from the opmsgr 2007 R2 RC version to the Opsmgr 2007 R2 RTM version be carefull with:

  * third party extensions like the Savision live maps for example. You will first need to uninstall the extensions and reinstall them afterwarts. You can download the extensions from <http://savision.com/download>
  * Also check that no opmsgr 2007 agents are installed on the same box. You will need to uninstall the agents prior to be able to upgrade the console

&nbsp;

Next, There is no upgrade path from the opsmgr authoring console 2007 RC to the R2 version:

&nbsp;

Oringal authoring console verions:

[<img height="244" width="220" src="http://scug.be/scom/files/2012/06/clip_image001_thumb_43834B61.jpg" alt="clip_image001" border="0" style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" />](http://scug.be/scom/files/2012/06/clip_image001_38C5F40C.jpg)

Upgrade:

[<img height="163" width="244" src="http://scug.be/scom/files/2012/06/clip_image003_thumb_62C5F234.jpg" alt="clip_image003" border="0" style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" />](http://scug.be/scom/files/2012/06/clip_image003_1C49022C.jpg)

Did an uninstall of the old one and install of the new authoring console:

[<img height="244" width="221" src="http://scug.be/scom/files/2012/06/clip_image004_thumb_2223A5C5.jpg" alt="clip_image004" border="0" style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" />](http://scug.be/scom/files/2012/06/clip_image004_17664E70.jpg)

&nbsp;

Why provide an upgrade path for the Operations console but not for the authoring console???

grtz,

Alexandre Verkinderen
