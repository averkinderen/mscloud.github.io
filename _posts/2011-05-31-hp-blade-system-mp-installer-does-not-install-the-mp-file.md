---
id: 648
title: HP Blade System MP installer does not install the mp file
date: 2011-05-31T05:16:50+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2011/05/31/hp-blade-system-mp-installer-does-not-install-the-mp-file.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1954"
  - "1954"
  - "1954"
  - "1954"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - HP
  - Management Pack
  - Operations Manager 2007
  - Opmsgr 2007 R2
  - opsmgr
  - opsmgr R2
---
If you want to use the latest HP blade management pack 1.40 you need to install or upgrade your HP proliant MP first to the same version 1.40.

[<img style="border-right-width: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_35C5A92D.png" width="244" height="67" />](http://scug.be/scom/files/2012/06/image_043A3B98.png)

The documentation doesn’t really say but it’s crucial. If you don’t install the Proliant mp first the Blade System MP installer will not import the blade management pack or even install it locally.

thanks,

Alexandre Verkinderen
