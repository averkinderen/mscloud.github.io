---
id: 2151
title: Upgrade Opsmgr 2007 R2 RC to Opsmgr 2007 R2 RTM
date: 2009-05-23T11:46:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2009/05/23/upgrade-opsmgr-2007-r2-rc-to-opsmgr-2007-r2-rtm.aspx
permalink: /upgrade-opsmgr-2007-r2-rc-to-opsmgr-2007-r2-rtm-2/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2935"
  - "2935"
  - "2935"
  - "2935"
  - "2935"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Opmsgr 2007 R2
  - Opmsgr 2007 R2 RC
  - opsmgr R2
  - upgrade
---
I&rsquo;ve several production environmnets running the Opmsgr 2007 R2 Release Candidate version. Now that the Opsmgr 2007 R2 Rtm is available I wanted to test the upgrade from RC to RTM in my lab environment before upgrading my production environments.

Start the SetupOM.exe

&nbsp;

[<img height="190" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_38C59351.png" alt="image" border="0" style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" />](http://scug.be/scom/files/2012/06/image_052D4CC0.png)

the setup will detect that you run on &ldquo;older&rdquo; version of opsmgr2007

[<img height="185" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_76DEAE02.png" alt="image" border="0" style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" />](http://scug.be/scom/files/2012/06/image_77B713EC.png)

The prerequisiter check failed because of the savision livemaps RC extensions:

[<img height="184" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_4BD69A30.png" alt="image" border="0" style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" />](http://scug.be/scom/files/2012/06/image_43A27499.png)

&nbsp;

Uninstall the savision rc extensions and your ready to go:

[<img height="188" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_6968752F.png" alt="image" border="0" style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" />](http://scug.be/scom/files/2012/06/image_4A25CE5C.png)

&nbsp;

After upgrading backup your encription key.

&nbsp;

[<img height="177" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_5854217F.png" alt="image" border="0" style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" />](http://scug.be/scom/files/2012/06/image_4F943F00.png)

&nbsp;

Don&rsquo;t forget to approve the agent pending update

[<img height="79" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_7FCAEDE9.png" alt="image" border="0" style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" />](http://scug.be/scom/files/2012/06/image_69584F62.png)

&nbsp;

After the upgrade from SCOM&nbsp;R2&nbsp;RC to R2 RTM you can&nbsp; reinstall the Savision Livemaps RC extensions from <http://www.savision.com/download>&nbsp;. Savision confirms that the Livemaps RC extensions works on SCOM 2007 R2 RTM and that they will release an update within a few weeks to fully support the new SCOM 2007 R2 and add some new functionalities.

Now that I&rsquo;m sure the upgrade from RC to R2 works like a charm I can upgrade my other RC environments at customers sites!

&nbsp;

Grtz,

Alexandre Verkinderen