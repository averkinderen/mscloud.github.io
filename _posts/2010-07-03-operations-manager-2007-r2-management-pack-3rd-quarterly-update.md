---
id: 629
title: Operations Manager 2007 R2 Management Pack 3rd quarterly update
date: 2010-07-03T09:02:05+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2010/07/03/operations-manager-2007-r2-management-pack-3rd-quarterly-update.aspx
permalink: /operations-manager-2007-r2-management-pack-3rd-quarterly-update/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1695"
  - "1695"
  - "1695"
  - "1695"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Management Pack
  - Operations Manager 2007
  - opsmgr
  - opsmgr R2
---
Microsoft released a week ago the 3<sup>rd</sup> quarterly update for the System Center Operations Manager 2007 R2 management pack. You can download it from here [http://www.microsoft.com/downloads/details.aspx?FamilyID=61365290-3c38-4004-b717-e90bb0f6c148&displaylang=en](http://www.microsoft.com/downloads/details.aspx?FamilyID=61365290-3c38-4004-b717-e90bb0f6c148&displaylang=en "http://www.microsoft.com/downloads/details.aspx?FamilyID=61365290-3c38-4004-b717-e90bb0f6c148&displaylang=en")

&#160;

The localization issue with the System Center Core reports (as described here [http://thoughtsonopsmgr.blogspot.com/2010/05/scom-r2-system-center-core-reporting.html](http://thoughtsonopsmgr.blogspot.com/2010/05/scom-r2-system-center-core-reporting.html "http://thoughtsonopsmgr.blogspot.com/2010/05/scom-r2-system-center-core-reporting.html") ) is solved as well.

&#160;

**Feature Summary**  
The Operations Manager 2007 R2 Management Packs includes the following features:

  * **Local and Remote Monitoring of an Agent’s Health** 
      * Operations Manager agents monitor themselves for events and performance indicators that signal an issue with the agent’s health. 
      * Management servers also maintain an external perspective of an agent’s health via the Health Service Watcher. 
      * The ‘Agent Health State’ view provides a side-by-side dashboard of both perspectives on the agent. 
  * **Optional, Automatic Agent Remediation Capabilities** 
      * If the Health Service Watcher determines that an agent is unhealthy, a series of diagnostics and recoveries can be enabled to further diagnose the problem and event take actions to attempt to fix the problem (e.g. Ping the server to see if it is completely offline, start a stopped agent, trigger a reinstall, etc.). Refer to the management pack guide for more details. 
      * Agents are monitoring their own process to ensure that memory utilization is not sustained at unacceptable levels. If this condition is detected then the agent will automatically restart itself to force the freeing up of memory. 
  * **Detection of Problems and Misconfigurations with Run As Accounts and Profiles** 
      * Checks are run on a regular basis to detect if any of the management group’s “Windows” type Run As Accounts have credentials which are about to expire. Alerts will be raised, and where possible this will be done in advance of the credentials expiring to avoid outages. 
      * Alerts will be raised if any errors are encountered during the distribution of Run As Accounts. 
  * **Monitoring of problems with Running Workflows in Management Packs** 
      * Numerous rules are provided to detect if workflows within management packs are failing. Examples of workflows include discoveries, rules, monitors, etc. Failures can range from bad configurations on the workflows themselves, script failures, permissions problems, etc. 
  * **Reports for identify drivers of data volumes in your environment** 
      * Introduced with the 6.1.7599.0 release of the management pack, these reports provide insight into the overall data volumes being processed by your environments. These reports can be used for gaining an understanding of current usage levels in order to establish a baseline and for identifying opportunities for tuning. 
  * **Operational Data Reporting** 
      * Introduced in the 6.1.7599.0 release of the management pack, these reports gather information and sends reports to Microsoft on a weekly basis (if you select to send reports). Microsoft uses these reports to improve the quality of its management packs and Operations Manager 2007. Participation in the program is strictly voluntary. For more information, see the Management Pack Guide. 

&#160;

Hope this helps,

Alexandre Verkinderen
