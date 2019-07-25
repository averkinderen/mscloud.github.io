---
id: 19675
title: Configuration of Opsmgr Exchange 2007 management pack
date: 2008-09-06T07:51:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2008/09/06/opsmgr-exchange-2007-management-pack.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2966"
  - "2966"
  - "2966"
  - "2966"
  - "2966"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Exchange
  - Management Pack
  - Operations Manager 2007
  - opsmgr
  - scom
---
Here are some guidelines if you want to import the Exchange 2007 management pack in your scom environment:

##### **Requirements**

This Management Pack requires the Operations Manager 2007 updates specified in Knowledge Base articles <a href="http://support.microsoft.com/kb/950853/en-us" target="_blank">950853</a>, <a href="http://support.microsoft.com/kb/951979/en-us" target="_blank">951979</a> and <a href="http://support.microsoft.com/kb/951380/en-us" target="_blank">951380</a> (see the Management Pack Guide for details).

Ensure that all systems running Exchange Server 2007 that are managed by Operations Manager use Local System as the Agent Action Account 

  * If you are monitoring Exchange Server 2007 clusters, ensure that all physical nodes of the cluster are monitored by Operations Manager 2007 and that Agent Proxy is turned on for each physical node in the cluster. 
  * Install the agent update specified in Knowledge Base article 950853 on all Exchange-based servers managed by Operations Manager before importing the Exchange Server 2007 Management Pack. This update addresses an agent memory leak issue. 
  * Install the update specified in Knowledge Base article 951979. This update contains an updated agent restart script and fixes issues with cluster discovery. 
  * If you are monitoring Exchange Server 2007 clusters, ensure that you have installed the agent update specified in Knowledge Base article 951380 on all Exchange Server 2007 cluster nodes managed by Operations Manager. This update addresses an issue with cluster discovery.

&nbsp;

Configuration is required for the following monitoring scenarios:

· ActiveSync (Test-ActiveSyncConnectivity)

· Outlook Web Access (Test-OWAConnectivity)

· Web Services (Test-WebServicesConnectivity)

· Remote Unified Messaging (Test-UMConnectivity)

##### <a class="" title="_Toc203976006" name="_Toc203976006"></a>Enabling Outlook Web Access, Exchange ActiveSync, and Exchange Web Services Connectivity

Test-OwaConnectivity, Test-ActiveSyncConnectivity, and Test-WebServicesConnectivity are the cmdlets used by the Exchange Server 2007 Management Pack to test Microsoft Office Outlook Web Access, Exchange ActiveSync, and Exchange Web Services connectivity from Client Access servers to Mailbox servers. The cmdlets require that a test mailbox be created on each Exchange Server 2007 Mailbox server that is to be tested.

To create the test mailbox, log on to the Exchange Server 2007 Mailbox server with a user account that is both an Exchange administrator and an Active Directory administrator. Open the Exchange Management Shell, locate the Scripts directory under the installation path for Exchange Server 2007 (usually Program FilesMicrosoftExchange ServerScripts) and execute the script New-TestCasConnectivityUser.ps1. Repeat this process on each Exchange Server 2007 Mailbox server that is to be tested. Note that if you have several organizational units named “Users” in your directory, you will need to specify the organizational unit in which to store the user.

c:Program FilesMicrosoftExchange ServerScriptsNew-TestCasConnectivityUser.ps1

[<img src="http://scug.be/blogs/scom/WindowsLiveWriter/OpsmgrExchange2007managementpack_87BD/image_thumb_2.png" style="border-width: 0px" alt="image" width="224" border="0" height="244" />](http://scug.be/blogs/scom/WindowsLiveWriter/OpsmgrExchange2007managementpack_87BD/image_6.png)

**Note:**

****

Pass=> must meet AD complexity

****

OU=Users,DC=dolmen,DC=be

**Results:**

[<img src="http://scug.be/blogs/scom/WindowsLiveWriter/OpsmgrExchange2007managementpack_87BD/image_thumb_1.png" style="border-width: 0px" alt="image" width="223" border="0" height="244" />](http://scug.be/blogs/scom/WindowsLiveWriter/OpsmgrExchange2007managementpack_87BD/image_4.png)

##### <a class="" title="_Toc203976007" name="_Toc203976007"></a>Enabling External Outlook Web Access Connectivity Monitoring

The rule is enabled by default. However, you must set an external URL on your Outlook Web Access virtual directory. To set an external URL, you must run the Set-OwaVirtualDirectory Exchange Management Shell command. The syntax of the command is: set-owavirtualdirectory &#8220;<Server name>owa (Default Web site)&#8221; -externalurl:&#8221;https://<Fully Qualified Domain Name>/owa&#8221;

**Note :**

The examples assume that SSL is enabled. If SSL is not enabled, use http:// instead of https://.

**powershell command:**

set-owavirtualdirectory &#8220;Exchange1owa (Default Web site)&#8221; -externalurl:https://Exchange1.dolmen.be/owa

[<img src="http://scug.be/blogs/scom/WindowsLiveWriter/OpsmgrExchange2007managementpack_87BD/image_thumb.png" style="border-width: 0px" alt="image" width="244" border="0" height="124" />](http://scug.be/blogs/scom/WindowsLiveWriter/OpsmgrExchange2007managementpack_87BD/image_2.png)

****

Greetz,

Alexandre Verkinderen

<http://scug.be/blogs/scom>

&nbsp;

<div class="wlWriterSmartContent" style="margin: 0px;padding: 0px">
  Tags van Technorati: <a href="http://technorati.com/tags/opsmgr" rel="tag">opsmgr</a>,<a href="http://technorati.com/tags/scom" rel="tag">scom</a>,<a href="http://technorati.com/tags/management%20pack" rel="tag">management pack</a>,<a href="http://technorati.com/tags/exchange" rel="tag">exchange</a>
</div>
