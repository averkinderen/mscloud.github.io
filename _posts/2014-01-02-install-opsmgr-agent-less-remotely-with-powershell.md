---
id: 742
title: Install OpsMgr Agent-less remotely with Powershell
date: 2014-01-02T14:04:00+10:00
author: alexandre@verkinderen.com

guid: http://scug.be/scom/?p=742
sc_member_order:
  - "0"
post_views_count:
  - "2502"
  - "2502"
  - "2502"
categories:
  - Powershell
  - SystemCenter
tags:
  - opsmgr
  - opsmgr 2012
  - powershell
  - system center
---
In our <a href="http://scug.be/scom/?p=738" target="_blank">previous post</a> we installed the OpsMgr agent remotely with Poweshell and enabled agent proxying. Now we are going to monitor a server agentless via Powershell:

[xml]

#=======================================================================  
#

# NAME: Opsmgr 2012 Agent-less Install

#

# AUTHOR: Alexandre Verkinderen

# DATE  : 10/23/2013

#  
#Requirements: The Operations Manager Powershell module needs to be installed  
#

# COMMENT: This script is designed to install OpsMgr 2012 agent-less

# The following need agent-less installation using default options: Add-SCOMAgentlessManagedComputer <a href="http://technet.microsoft.com/en-us/library/hh918462.aspx">http://technet.microsoft.com/en-us/library/hh918462.aspx</a> : SCDPM01, SCCM01

#=======================================================================

#Variables  
$MS = "SCOM01.contoso.com"

invoke-command -ComputerName $MS{  
$AgentList = @("scdpm01.contoso.com","sccm01.contoso.com")  
$MS = "SCOM01.contoso.com"

#Import PowerShell Modules  
import-module OperationsManager  
#Connect to OpsMgr Management Group  
New-SCOMManagementGroupConnection -ComputerName $MS

#&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;  
#OpsMgr Agent Installation  
#&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

Foreach($Agent in $AgentList)  
{

Add-SCOMAgentlessManagedComputer -Name $Agent -ManagedByManagementServer (Get-SCOMManagementserver -Name $MS)

}  
}

[/xml]

Thanks,

Alexandre Verkinderen
