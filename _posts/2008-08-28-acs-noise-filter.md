---
id: 19674
title: ACS noise filter
date: 2008-08-28T14:55:05+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2008/08/28/acs-noise-filter.aspx
permalink: /acs-noise-filter/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2139"
  - "2139"
  - "2139"
  - "2139"
  - "2139"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - acs
  - audit collection service
  - manuals
  - Operations Manager 2007
  - opsmgr
  - scom
  - secure vantage
---
When you install ACS you will get a ton of events! Not all events are relevant for your environment. <a href="http://www.securevantage.com/" target="_blank">Securevantage</a> has written a nice <a href="http://www.securevantage.com/Products/2007%20Solutions/Docs/ACS%20Guides/Secure%20Vantage%20ACS%20Noise%20Filter%20Guide.pdf" target="_blank">noisefilter</a> guide. This guide introduces noise filters for Windows Servers 2000 & 2003 Security Events.

&nbsp;

Also interesting is the&nbsp; Secure Vantage <a href="http://www.securevantage.com/Products/2007%20Solutions/Docs/Secure%20Vantage%20Windows%20Security%20Auditing%20Reference%20List.xls" target="_blank">Security Auditing Reference List</a>: Over 1300 Windows security events and settings with interactive links to Randy Franklin Smiths online security wiki.

The Service Account Authentication Success filter provides an example of how to filter specific user accounts or&nbsp; patterns within a user account name like admin or sys on logon. These are commonly used to filter service accounts that run on all systems frequently such as antivirus or backup programs. Please note this is for ‘Success’ activity only, all Logon failure activity should be collected.

<a name="_Toc207617005"><a href="http://scug.be/blogs/scom/WindowsLiveWriter/ACSnoisefilter_E4EE/image_4.png"><img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="244" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/ACSnoisefilter_E4EE/image_thumb_1.png" width="219" border="0" /></a></a>

&nbsp;

Run adtamin:

AdtAdmin.exe /getquery

Result: Current query: &#8216;select * from AdtsEvent&#8217;

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="123" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/ACSnoisefilter_E4EE/image_thumb.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/ACSnoisefilter_E4EE/image_2.png)

&nbsp;

Next, set the query to drop the &#8220;sys&#8221; and &#8220;adm&#8221; logons:

AdtAdmin.exe /setquery /query:&#8221;Select * from AdtsEvent where NOT ((HEADERUSER LIKE &#8216;%ADM\_%&#8217; OR HEADERUSER LIKE &#8216;%SYS\_%&#8217;) AND(EventID = 528 OR EventID = 540 OR EventID = 680))&#8221;

&nbsp;

check your query by running AdtAdmin.exe /getquery. the result should be:

Current query: &#8220;Select * from AdtsEvent where NOT ((HEADERUSER LIKE &#8216;%ADM\_%&#8217; OR HEADERUSER LIKE &#8216;%SYS\_%&#8217;) AND(EventID = 528 OR EventID = 540 OR EventID = 680))&#8221;

&nbsp;

Now all these events will be dropped before they enter the acs database.

&nbsp;

Greetz,

Alexandre Verkinderen

<http://scug.be/blogs/scom>

&nbsp;

<div class="wlWriterSmartContent" style="padding-right: 0px;padding-left: 0px;padding-bottom: 0px;margin: 0px;padding-top: 0px">
  Tags van Technorati: <a href="http://technorati.com/tags/acs" rel="tag">acs</a>,<a href="http://technorati.com/tags/audit%20collection%20service" rel="tag">audit collection service</a>,<a href="http://technorati.com/tags/opmsgr" rel="tag">opmsgr</a>,<a href="http://technorati.com/tags/scom" rel="tag">scom</a>
</div>
