---
id: 719
title: Powershell Deployment Toolkit and WAP
date: 2013-12-03T14:50:00+10:00
author: alexandre@verkinderen.com

guid: http://scug.be/scom/?p=719
permalink: /powershell-deployment-toolkit-and-wap/
sc_member_order:
  - "0"
post_views_count:
  - "1953"
  - "1953"
  - "1953"
  - "1953"
categories:
  - Azure
  - SystemCenter
tags:
  - powershell
  - powershell deployment toolkit
  - system center
  - WAP
  - XML
---
The latest publicly available PDT version <a href="http://blogs.technet.com/b/privatecloud/archive/2013/10/17/deployment-pdt-update-for-system-center-2012-r2-now-available.aspx" target="_blank">2.5.270</a> now includes besides System Center 2012 R2 also Windows Azure Pack.

You can find the new WAP roles in the Variable.xml as shown below:

[<img style="padding-top: 0px; padding-left: 0px; margin: 0px 0px 15px; padding-right: 0px; border-width: 0px;" title="clip_image002" alt="clip_image002" src="http://www.mscloud.be/wp-content/uploads/2013/11/clip_image002_thumb11.jpg" width="644" height="133" border="0" />](http://www.mscloud.be/wp-content/uploads/2013/11/clip_image00211.jpg)

You will notice that a few roles are missing like the SMA role. You can easily include the SMA Roles

  * System Center 2012 R2 Service Management Automation Web Service Server
  * System Center 2012 R2 Service Management Automation PowerShell Module
  * System Center 2012 R2 Service Management Automation Runbook Worker Server

by just copying the missing roles from the workflow.xml into your variable.xm like this:

[xml]<Role Name="System Center 2012 R2 Service Management Automation Runbook Worker Server" Component="System Center 2012 R2 Service Management Automation">[/xml]

[<img style="padding-top: 0px; padding-left: 0px; margin: 0px; padding-right: 0px; border: 0px;" title="image" alt="image" src="http://www.mscloud.be/wp-content/uploads/2013/11/image_thumb2.png" width="244" height="107" border="0" />](http://www.mscloud.be/wp-content/uploads/2013/11/image2.png)

Thanks to <a href="http://blogs.technet.com/b/privatecloud/" target="_blank">Rob Willis</a> for pointing this out to me.

Alexandre Verkinderen
