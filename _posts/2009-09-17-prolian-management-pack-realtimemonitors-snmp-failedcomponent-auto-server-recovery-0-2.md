---
id: 2341
title: Proliant Management pack RealtimeMonitors_SNMP.FailedComponent Auto Server Recovery 0
date: 2009-09-17T12:17:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2009/09/17/prolian-management-pack-realtimemonitors-snmp-failedcomponent-auto-server-recovery-0.aspx
permalink: /prolian-management-pack-realtimemonitors-snmp-failedcomponent-auto-server-recovery-0-2/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1739"
  - "1739"
  - "1739"
  - "1739"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - HP
  - Issue
  - Operations Manager 2007
  - Opmsgr 2007 R2
  - opsmgr
  - scom
---
Just imported the HP Proliant management pack for SCOM 2007 and hade a lot of servers in warning state even if nothing was wrong in the Insight homepage.

[<img style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_55594CE6.png" width="244" border="0" height="90" />](http://scug.be/scom/files/2012/06/image_2F610BDF.png)

&nbsp;

So I opened the healthexplorer and found RealtimeMonitors_SNMP.FailedComponent Auto Server Recovery 0&nbsp; in warning state.

[<img style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" alt="clip_image002" src="http://scug.be/scom/files/2012/06/clip_image002_thumb_5FD43DFD.jpg" width="244" border="0" height="183" />](http://scug.be/scom/files/2012/06/clip_image002_2C513E9B.jpg)

After investigating I found that problem was that the ASR was not configured on some servers and needs to be enable.

[<img style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" alt="clip_image004" src="http://scug.be/scom/files/2012/06/clip_image004_thumb_6BFD6A37.jpg" width="244" border="0" height="132" />](http://scug.be/scom/files/2012/06/clip_image004_03FC293E.jpg)

&nbsp;

&nbsp;

Hope this helps,

Alexandre Verkinderen