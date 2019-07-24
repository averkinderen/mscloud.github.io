---
id: 549
title: RMS grayed out and server discovery failed
date: 2009-02-11T15:08:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2009/02/11/rms-grayed-out-and-server-discovery-failed.aspx
permalink: /rms-grayed-out-and-server-discovery-failed/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1762"
  - "1762"
  - "1762"
  - "1762"
  - "1762"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - General
  - Issue
  - Operations Manager 2007
  - opsmgr
  - RMS
  - scom
---
After I installed my RMS and OpsmgrDB on two different servers my root management server went gray and every 10 minutes or so I receive an alert stating the RMS is unavailable.&nbsp; Usually these close within a minute but some times take up to 10 minutes.&nbsp; 

Below is the alert I receive.

Alert: Root Management Server Unavailable.  
Source: (my server name)  
Path: (my server name)  
Last modified by: System  
Last modified time: 2/1/2008 4:19:53 PM  
Alert description: The root management server (Healthservice) has stopped  
heartbeating soon after Fri, 01 Feb 2008 23:17:29 GMT. This adversely affects  
all availability calculation for the entire management group.

&nbsp;

[<img border="0" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/problem_thumb.png" alt="problem" height="200" style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/problem_2.png)

Also got the following error when I wanted to discover and install agents on my server:

&#8220;An exception was thrown while processing LaunchDiscovery for session id uuid:57e9b453-4e4f-465c-9c48-c8d7d209e747;id=5.&nbsp; Exception Message: The creator of this fault did not specify a Reason.  
Full Exception: System.ServiceModel.FaultException\`1&#8243;

&nbsp;

[<img border="0" width="220" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb.png" alt="image" height="244" style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" />](http://scug.be/scom/files/2012/06/image_2.png)

&nbsp;

I checked the time on my RMS Server and on the SQL server and there was a 3 minute delay!

&nbsp;

The resolution was to resync the time on both servers with the following command

NET TIME %LOGONSERVER% /SET /Y

&nbsp;

After the resync everything went fine!! My rms went green and I could discover and install my agents again!!

&nbsp;

Grtz,

Alexandre Verkinderen

ps: thx to David Biot, my pupil 😉