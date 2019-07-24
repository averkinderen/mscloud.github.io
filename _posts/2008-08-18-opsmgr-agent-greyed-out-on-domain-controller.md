---
id: 517
title: Opsmgr agent grayed out on domain controller
date: 2008-08-18T13:41:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2008/08/18/opsmgr-agent-greyed-out-on-domain-controller.aspx
permalink: /opsmgr-agent-greyed-out-on-domain-controller/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1672"
  - "1672"
  - "1672"
  - "1672"
  - "1672"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Essentials
  - Issue
  - Operations Manager 2007
  - opsmgr
  - scom
---
Last week I deployed my scom agents on my domain controllers. The installation was succesful and of course I checked the agent proxing checkbox in the administration console.

&nbsp;

After 30 minutes I checked the status of my agent and it was grayed out!! So I looked at the event log of my dc and saw this error

&nbsp;

Event Type: Error

Event Source: HealthService

Event Category: Health Service

Event ID: 7017

Date: 4/07/2008

Time: 11:49:36

User: N/A

Computer:

Description:

The health service blocked access to the windows credential NT AUTHORITYSYSTEM because it is not authorized on management group dgz. You can run the HSLockdown tool to change which credentials are authorized.

For more information, see Help and Support Center at http://go.microsoft.com/fwlink/events.asp.

<http://technet.microsoft.com/en-us/library/bb309542(TechNet.10).aspx>

On computers requiring high security, for example a domain controller, you may need to deny certain identities access to rules, tasks, and monitors that might jeopardize the security of your server

So, you have to run the HSlockdown tool to change the credentials that are authorized:

[<img height="213" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/Opsmgragentgreyedoutondomaincontroller_DCB5/image_thumb.png" width="422" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/Opsmgragentgreyedoutondomaincontroller_DCB5/image_2.png)&nbsp;

When you run HSLockdown [ManagementGroupName] /L &#8211; List Accounts/groups you can see that the system account is denied! Thats why my agents are greyed out!

[<img height="137" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/Opsmgragentgreyedoutondomaincontroller_DCB5/image_thumb_1.png" width="271" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/Opsmgragentgreyedoutondomaincontroller_DCB5/image_4.png)

Next run HSLockdown [ManagementGroupName] /R &#8220;NT AUTHORITYSYSTEM&#8221;

Restart your healthservice and you&#8217;re done!!

Greetz,

Alexandre Verkinderen

[http://scug.be/blogs](http://scug.be/blogs "http://scug.be/blogs")