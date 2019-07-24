---
id: 1611
title: How to find match the GUID to an Opsmgr agent
date: 2008-07-17T15:23:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2008/07/17/how-to-find-match-the-guid-to-an-agent.aspx
permalink: /how-to-find-match-the-guid-to-an-agent-2/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1466"
  - "1466"
  - "1466"
  - "1466"
  - "1466"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Operations Manager 2007
  - opsmgr
  - scom
  - sql
---
[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="76" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/HowtofindmatchtheGUIDtoanagent_12346/image_thumb.png" width="448" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/HowtofindmatchtheGUIDtoanagent_12346/image_2.png)

Start SQL management Studio, connect to the OperationsManager Database and run the following query

Select * from BaseManagedEntity where BaseManagedEntityID = &#8216;first guid in the alert&#8217;

In our case the query is&nbsp; Select * from BaseManagedEntity where BaseManagedEntityID = &#8216;D7463D6E-F334-40C3-3A86-C68A77D36BF8 &#8216;

Thx to <a href="http://msmvps.com/blogs/opsmgr/default.aspx" target="_blank">Yann Gainche</a>.

Greetz,  
Alkin