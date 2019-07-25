---
id: 630
title: Service Manager Management Pack
date: 2010-07-03T09:42:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2010/07/03/service-manager-management-pack.aspx
permalink: /service-manager-management-pack/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2007"
  - "2007"
  - "2007"
  - "2007"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Management Pack
  - Operations Manager 2007
  - opsmgr
  - opsmgr R2
  - Service Manager
---
Microsoft released the Service Manager 2010 Management Pack. The Microsoft System Center Service Manager 2010 Management Pack helps you manage your Service Manager infrastructure by monitoring the health of the Service Manager management servers and services.

&nbsp;

**Features**:

  * Capturing critical events from Service Manager and creating corresponding alerts in System Center Operations Manager 2007 R2.
  * Monitoring the health of vital Service Manager services and providing users with a real-time health status.
  * Providing Operations Manager integrated knowledge for events.
  * Ensuring that the management pack provides clear health information, and that it is extendible, allowing users to add objects such as monitors, overrides, tasks, and knowledge.

&nbsp;

<a name="_Toc265152337"><strong>Supported Configurations</strong></a><a name="zd75f2a0a038841db882d7dd796eff18a"></a>

Service Manager Management Pack 7.0.5826.856 supports all configurations that are supported by Microsoft System Center Service Manager 2010.

Service Manager supports SQL Server clustering for the databases, and Network Load Balancing (NLB) for the Service Manager management servers and portals. In these topologies, the individual parts are monitored individually regardless of the existence of NLB.

Supported Configurations

The following table details the supported configurations for the Service Manager Management Pack.

<table cellpadding="0" cellspacing="0" border="1">
  <tr>
    <td width="295" valign="top">
      Configuration
    </td>
    
    <td width="295" valign="top">
      Support
    </td>
  </tr>
  
  <tr>
    <td width="295" valign="top">
      Service Manager management servers
    </td>
    
    <td width="295" valign="top">
      Yes, all supported configurations and all supported deployment topologies
    </td>
  </tr>
  
  <tr>
    <td width="295" valign="top">
      Servers on which workflows run
    </td>
    
    <td width="295" valign="top">
      Yes
    </td>
  </tr>
  
  <tr>
    <td width="295" valign="top">
      Data warehouse management servers
    </td>
    
    <td width="295" valign="top">
      Yes
    </td>
  </tr>
  
  <tr>
    <td width="295" valign="top">
      Clustered servers
    </td>
    
    <td width="295" valign="top">
      Yes
    </td>
  </tr>
  
  <tr>
    <td width="295" valign="top">
      Agentless monitoring
    </td>
    
    <td width="295" valign="top">
      No
    </td>
  </tr>
  
  <tr>
    <td width="295" valign="top">
      Virtual environment
    </td>
    
    <td width="295" valign="top">
      Yes
    </td>
  </tr>
</table>

&nbsp;

You can download the mp here [http://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=82a6cd07-85aa-4739-9829-f1e7cdea7fe7](http://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=82a6cd07-85aa-4739-9829-f1e7cdea7fe7 "http://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=82a6cd07-85aa-4739-9829-f1e7cdea7fe7")

Also have look at the blog post of Darko Vukovic he&#8217;s <a target="_blank" href="http://blogs.technet.com/b/servicemanager/archive/2010/06/30/best-practices-service-manager-2010-management-pack-for-operations-manager-2007-r2.aspx" title="Best Practices: Service Manager 2010 management pack for operations manager 2007 R2">posted</a>&nbsp;a very useful accompanying set of best practices for getting started with&nbsp;the new management pack.
