---
id: 508
title: 'Upgrading SCCM 2007 RTM to SCCM 2007 SP1 : Lessons Learned'
date: 2008-06-30T20:10:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2008/06/30/upgrading-sccm-2007-rtm-to-sccm-2007-sp1-lessons-learned.aspx
permalink: /upgrading-sccm-2007-rtm-to-sccm-2007-sp1-lessons-learned/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1440"
  - "1440"
  - "1440"
  - "1440"
  - "1440"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Uncategorized
---
Today at a customer I ran into some serious problems after applying SP1 for SCCM 2007 .

&nbsp;During applying SP1 for SCCM 2007 , the server crached and rebooted . After the reboot I had noticed that the SCCM enviroment wasn&#8217;t stable anymore. I tryed to relaunch the setup

I try to put some steps online to help or guide you to make sure that you will make it to the finish.

  1. First of all you will need to make a backup of your Database under SQL 2005.But I discovered soon enough that you aren&#8217;t anything with the DB only .</p> 
  2. Make sure you have a recent backup of your primary site config settings . You find that one under your site settings .

  3. Make sure that you upgrade the SCCM RTM server to SP1 with the **SAME CREDENTIALS**&nbsp; as you installed the SCCM2007 RTM ! **Otherwise it WILL FAIL and CRIPLE the Site** .

  4. Make sure that you

&nbsp;

&nbsp;

While it&#8217;s a simple process to install the console, you DO know that for every version of SMS / SCCM that provides a SP, you need to update not only the client&#8217;s. but the console too. This has always been a pain point for me, but I wanted to share an issue I ran across last week after upgrading to SCCM SP1 to install the console.

Despite the proper configuration of SCCM connecting to the SQL Providor, we could not connect on some machines. The solution was as follows:

  1. Open Computer Management and open WMI at the bottom.</p> 
  2. Click on WMI and expand the WMI Control. Right click and choose properties. Select the Security Tab.

  3. Scroll down to the SMS WMI conrrol and grant the &#8220;Local SMS Admin&#8221; group for the server and give it full control.

  4. Under the SMS control will be the site control. You will need to add the same permission to the local site code.

Once you have completed this, your admins or users of the control panel should have the access needed to connect to the SQL providor.

Hope this helps someone out there&#8230;.