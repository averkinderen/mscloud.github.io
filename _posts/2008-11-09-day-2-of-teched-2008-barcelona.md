---
id: 538
title: Day 2 of teched 2008 Barcelona
date: 2008-11-09T11:08:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2008/11/09/day-2-of-teched-2008-barcelona.aspx
permalink: /day-2-of-teched-2008-barcelona/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1485"
  - "1485"
  - "1485"
  - "1485"
  - "1485"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Events
  - Operations Manager 2007
  - opsmgr
  - opsmgr R2
  - scom
  - teched
---
At day 2 one of the sessions I followed covered the future of opsmgr. They announced that at the end of this month the beta of Opsmgr R2 will be available, RC is for Q1 of 2009 and RTM in Q2 2009. For opsmgr 10, the next version we will have to wait until H1 of 2011.

&nbsp;

Microsoft also announced the availabiltity of opsmgr R2 on their website:

##### System Center Operations Manager 2007 R2 will introduce new and enhanced capabilities including extending its monitoring capabilities to Unix and Linux servers and workloads, the ability to report on service levels across IT availability and performance, enhanced system and web monitoring capabilities, and more.

The Operations Manager 2007 R2 Beta will be available for public download towards the end of November 2008, through Microsoft Connect.&nbsp; Please check back soon for more information on how to obtain this exciting new beta, and see the [System Center Blog](http://blogs.technet.com/systemcenter/) for announcements and updates.

##### Product Overview

[<img alt="Datasheet: Monitoring Cross Platform environments with System Center Operations Manager 2007 R2" src="http://i.technet.microsoft.com/dd239186.articles_20%28en-us,MSDN.10%29.gif" align="left" border="0" />](http://download.microsoft.com/download/3/a/0/3a07504e-905e-4ae4-8e46-564b774cd354/OpsMgrCrossPlatDS_Aug2008.pdf)  
[**Datasheet: Monitoring Cross Platform environments with System Center Operations Manager 2007 R2**](http://download.microsoft.com/download/3/a/0/3a07504e-905e-4ae4-8e46-564b774cd354/OpsMgrCrossPlatDS_Aug2008.pdf)

Overview of the upcoming support for monitoring cross platform environments through the Operations Manager 2007 R2 Beta, including benefits, features, and supported environments.

[<img alt="White Paper: Managing Your Unix/Linux Systems with Operations Manager 2007 Cross Platform Extensions" src="http://i.technet.microsoft.com/dd239186.articles_20%28en-us,MSDN.10%29.gif" align="left" border="0" />](http://download.microsoft.com/download/3/4/f/34f0eb37-66fa-4245-9694-2fbabaf960fe/OpsMgrCrossPlatWP_Aug2008.pdf)  
[**White Paper: Managing Your Unix/Linux Systems with Operations Manager 2007 Cross Platform Extensions**](http://download.microsoft.com/download/3/4/f/34f0eb37-66fa-4245-9694-2fbabaf960fe/OpsMgrCrossPlatWP_Aug2008.pdf)

This paper discusses how Operations Manager 2007 R2, using its integrated Cross Platform Extensions, can help data centers and large IT organizations:

  * More easily identify and resolve issues in a cross-platform environment 
  * Manage both Microsoft and non-Microsoft environments as simply and efficiently as possible 
  * Improve service levels and visibility across Microsoft, Unix, and Linux platforms 

&nbsp;

### Here are some interessting new features of Opsmgr R2:

  * **enhanced servic level tracking** 
  * **proces monitor template :** 

Now you can monitor the wanted and unwanted running processes! This is a great feature, as a lot of my clients want this. So you will be able to not only monitor running services, but also processes. When for example opsmgr detected that an unwanted process is running you can run an automatically response to kill the process. But there is no auto resolving.

&nbsp;

  * **oledb monitor template improved** 
  * **performance and usability** 
      * management pack import: 

The way we import management packs is improved. Now I&rsquo;ve to go to the [mp download site](http://technet.microsoft.com/en-us/opsmgr/cc539535.aspx), downoad my mp, install it and import it. With opsmgr R2 you have the possibility to download and import the mp&rsquo;s directly from your console. So you have the choice to import a local mp or to use the webservice and search for mp&rsquo;s directly from your console. Opsmgr will automatically check for missing dependency&rsquo;s and propose the mp&rsquo;s you should import to resolve the problem. After you selected a category of mp&rsquo;s or a specific mp opmsgr will download the mp and import it.

&nbsp;

  * &nbsp; 
      * one click maintance mode: 

Now when it&rsquo;s required to physically power down a computer for maintenance. Now it&rsquo;s a 3 step process. You have to put the computer into maintance mode, the health service and the heatlh service watcher. You have some powershell scripts [that you can download](http://blogs.technet.com/cliveeastwood/archive/2007/09/18/agentmm-a-command-line-tool-to-place-opsmgr-agents-into-maintenance-mode.aspx)&nbsp; . With R2 you don&rsquo;t have to run any scripts anymore. You have to possibility to put an entire computer into maintance mode.

&nbsp;

  * &nbsp; 
      * agent proxing healthservce guid is resolved: 

Now you have to run a [sql query](/blogs/scom/archive/2008/07/17/how-to-find-match-the-guid-to-an-agent.aspx) or a powershell script to find the matching computer name of healthservice guid. Not anymore in R2!

&nbsp;

  * &nbsp; 
      * new overrides view : 

In R2 we will have a nice overrides summary page with all the overrides we created.

&nbsp;

  * &nbsp; 
      * Webconsole: 

Now we can use the healthexplorer into the web UI.

&nbsp;

  * **scalabilty** 

They have done a great job on the UI perfomance side. scrolling 2000 alerts is now running like a charm!

&nbsp;

  * **cross platform monitoring** 

Cross platform will be a part of the R2 installation. Microsoft is looking with some vendors to put a scom agent directly into the linux/solaris distribution. With the R2 version we will have some new specific templates to monitor unix services and unix/linux logfiles based on regular expressions. But now we have a nice test button to test our regullar expression!

&nbsp;

&nbsp;

Greetz,

Alexandre Verkinderen

<http://www.scug.be/blogs>