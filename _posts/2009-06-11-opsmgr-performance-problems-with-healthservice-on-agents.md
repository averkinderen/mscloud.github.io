---
id: 572
title: Opsmgr Performance problems with healthservice on agents
date: 2009-06-11T20:59:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2009/06/11/opsmgr-performance-problems-with-healthservice-on-agents.aspx
permalink: /opsmgr-performance-problems-with-healthservice-on-agents/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2148"
  - "2148"
  - "2148"
  - "2148"
  - "2148"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Agents
  - Issue
  - manuals
  - Operations Manager 2007
  - Opmsgr 2007 R2
  - opsmgr
  - opsmgr R2
  - Performance
  - scom
  - WMI
---
On some occasions the scom agent can cause a lot of performance issues on the servers. Here I will describe some steps I take when I have performance problems and in most of the cases it works for me.

The first thing you should do is to configure the antivirus exclusions for opsmgr. Have a look at Kevin Holman&rsquo;s blogpost <a href="http://blogs.technet.com/kevinholman/archive/2007/12/12/antivirus-exclusions-for-mom-and-opsmgr.aspx" target="_blank">Antivirus Exclusions for MOM and OpsMgr</a> on how to do this. Configuring anti virus exlusions will help you gain some performance.

This is a screenshot of the performance of my cpu before the anti virus exclusions:

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" alt="clip_image002[1]" src="http://scug.be/scom/files/2012/06/clip_image0021_thumb_253806C1.jpg" width="244" border="0" height="187" />](http://scug.be/scom/files/2012/06/clip_image0021_5F2749AD.jpg)

&nbsp;

And this one is after the anti virus exclusions:

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" alt="clip_image002[3]" src="http://scug.be/scom/files/2012/06/clip_image0023_thumb_76724E1E.jpg" width="244" border="0" height="182" />](http://scug.be/scom/files/2012/06/clip_image0023_44E6E089.jpg)

&nbsp;

The second thing is to have a look at the healthservice.exe. We&rsquo;ve created a collection performance rule in the <a href="/blogs/scom/archive/2009/06/08/collect-processor-time-of-the-healthservice-exe-of-your-agents.aspx" target="_blank">previous post</a> to collect the processor time % of the healthservice. If the healthservice is consuming more than 15 a 20 % of your cpu you have a problem . In my case I&nbsp; had huge performance problems due to the healthservice.exe that was taking all the processor time. My healthservices.exe was taking about 50 to 60 % with peaks to 100% on my agents&hellip;.You can imagine the reaction of my client&hellip;.he was not very happy.

Performance view of my healthservice.exe on one of my agents:

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" alt="clip_image001" src="http://scug.be/scom/files/2012/06/clip_image001_thumb_03D86125.jpg" width="69" border="0" height="244" />](http://scug.be/scom/files/2012/06/clip_image001_162127E7.jpg)

So I did some tests, installed all the necessary hotfixes, deleted the healthservice cache, exception of programfilesscom for the antivirus etc etc. But with no results.

So I tought it was WMI and did the following steps to rebuild the wmi:

&middot; Net Stop WinMgmt

&middot; Ren %WinDir%System32WbemRepository %WinDir%System32WbemOldRepository

&middot; Net Start WinMgmt

Still no success, still had performance troubles. I contacted one of our company architects who send me a <a href="/media/p/1088.aspx" target="_blank">repairwmi.cmd</a> &ldquo;program&rdquo; he developed . It will recompile all the mofiles, re-register all the dll&rsquo;s, exe&rsquo;s etc.

Steps to take:

  1. Copy the content of the repairwmi.cmd to the %WinDir%System32Wbem folder</p> 
  2. Run the repairwmi.cmd

  3. Stop the opsmgr healthservice

  4. Delete the healthservice cache

  5. Start the opsmgr healthservice

And voila! All my performance problems where gone!!

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" alt="clip_image002" src="http://scug.be/scom/files/2012/06/clip_image002_thumb_752DB53F.jpg" width="244" border="0" height="208" />](http://scug.be/scom/files/2012/06/clip_image002_11AAA720.jpg)

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" alt="clip_image003" src="http://scug.be/scom/files/2012/06/clip_image003_thumb_425DAECB.jpg" width="244" border="0" height="209" />](http://scug.be/scom/files/2012/06/clip_image003_29CE117B.jpg)

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" alt="clip_image004" src="http://scug.be/scom/files/2012/06/clip_image004_thumb_6F729B99.jpg" width="244" border="0" height="184" />](http://scug.be/scom/files/2012/06/clip_image004_543A4298.jpg)

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" alt="clip_image005" src="http://scug.be/scom/files/2012/06/clip_image005_thumb_398DA67F.jpg" width="244" border="0" height="211" />](http://scug.be/scom/files/2012/06/clip_image005_48385264.jpg)

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" alt="clip_image006" src="http://scug.be/scom/files/2012/06/clip_image006_thumb_1F4D3D5B.jpg" width="244" border="0" height="210" />](http://scug.be/scom/files/2012/06/clip_image006_6E2E02BA.jpg)

&nbsp;

As you can see this reduced drastically the processor time % of the healthservice!

&nbsp;

Hope this helps,

Alexandre Verkinderen
