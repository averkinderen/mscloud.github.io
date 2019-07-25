---
id: 3001
title: Powershell Deployment Toolkit failed missing port for sql server
date: 2013-11-28T20:28:04+10:00
author: alexandre@verkinderen.com

guid: http://scug.be/scom/?p=711
permalink: /powershell-deployment-toolkit-failed-missing-port-for-sql-server-2/
sc_member_order:
  - "0"
post_views_count:
  - "1838"
  - "1838"
  - "1838"
categories:
  - Uncategorized
tags:
  - pdt
  - powershell
  - powershell deployment toolkit
  - system center
---
During the validation of PDT I received the following errory saying that the port was missing for my new SQL instances:

[<img title="clip_image002" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="clip_image002" src="http://www.mscloud.be/wp-content/uploads/2013/11/clip_image002_thumb.jpg" width="644" height="197" />](http://www.mscloud.be/wp-content/uploads/2013/11/clip_image002.jpg)

To fix this just add Port="number" in the SQL instance section like shown below:

[<img title="image" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; padding-top: 0px; padding-left: 0px; border-left: 0px; display: inline; padding-right: 0px" border="0" alt="image" src="http://www.mscloud.be/wp-content/uploads/2013/11/image_thumb.png" width="644" height="149" />](http://www.mscloud.be/wp-content/uploads/2013/11/image.png)

Thanks for Damian Flynn to point this out to me.

Hope this helps,

Alex
