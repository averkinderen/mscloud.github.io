---
id: 507
title: Dell Management Pack Opsmgr Issue Solved!
date: 2008-06-30T18:00:37+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2008/06/30/dell-management-pack-issue-solved.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1804"
  - "1804"
  - "1804"
  - "1804"
  - "1804"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Uncategorized
---
I had a client with only Dell servers and moitored by Opsmgr 2007 SP1.

I imported the <a href="http://support.us.dell.com/support/downloads/download.aspx?fileid=229201" target="_blank">Dell management pack</a> and after a while I had this error:

Event Type: Error  
Event Source: HealthService  
Event Category: Health Service  
Event ID: 4000  
Date: <var>Date</var>  
Time: <var>Time</var>  
User: N/A  
Computer: <var>ComputerName</var>  
Description:  
A monitoring host is unresponsive or has crashed. The status code for the host  
failure was 2164195371.  
Problem signature:  
Problem Event Name: APPCRASH  
Application Name: MonitoringHost.exe  
Application Version: 6.0.6278.0  
Application Timestamp: 47b71437  
Fault Module Name: HealthServiceRuntime.dll  
Fault Module Version: 6.0.6278.0  
Fault Module Timestamp: 47b71433  
Exception Code: c0000005  
Exception Offset: 00003d9d  
OS Version: 6.0.6001.2.1.0.16.7  
Locale ID: 1033

Microsoft discovered an issue in the SNMP networking module that causes the HealthService to become unstable.

There is now a Microsoft [hotfix available](http://support.microsoft.com/?kbid=951526) to fix this error. You can&#8217;t download the hotfix so you have to contact <a href="http://support.microsoft.com/contactus/?ws=support" target="_blank">Microsoft Customer Service and Supp</a>ort to obtain the hotfix.

&nbsp;

When I installed the hotfix my issue was solved!

Greetz,

Alkin
