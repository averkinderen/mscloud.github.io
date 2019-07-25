---
id: 738
title: Install OpsMgr Agent remotely with Powershell
date: 2013-12-30T13:59:00+10:00
author: alexandre@verkinderen.com

guid: http://scug.be/scom/?p=738
permalink: /install-opsmgr-agent-remotely-with-powershell/
sc_member_order:
  - "0"
post_views_count:
  - "2004"
  - "2004"
  - "2004"
categories:
  - Powershell
  - SystemCenter
tags:
  - powershell
  - scom
  - scom 2012
  - system center
---
As you are aware by now I’m creating a series of Powershell automation activities to automate some System Center installation tasks. Below you can find a Powershell script that will connect to the Opsmgr server remotely (so you dont need the OpsMgr powershell snappin installed locally) deploy the scom agent and enable agent proxiyng on them.

[xml]

#=======================================================================  
#

# NAME: Opsmgr 2012 Agent Install

#

# AUTHOR: Alexandre Verkinderen

# DATE  : 10/23/2013

#

# Requirements: FIrewall needs to be disabled

#

# COMMENT: This script is designed to install OpsMgr 2012 agents.

# The following serfvers  need agents instaled using default options: Install-SCOMAgent <a href="http://technet.microsoft.com/en-us/library/hh920243.aspx:">http://technet.microsoft.com/en-us/library/hh920243.aspx:</a> DC01, SCVMM01

#=======================================================================

#Variables  
$MS = "SCOM01.contoso.com"

#Connect remotely to the SCOM server  
Invoke-Command -ComputerName $MS -ScriptBlock {

#Variables  
$MS = "SCOM01.contoso.com"  
$AgentList = @("dc01.contoso.com")  
$Password = ConvertTo-SecureString "Passw0rd!" -AsPlainText -Force  
$username = "contosoadministrator"  
$InstallAccount = New-Object System.Management.Automation.PSCredential($username,$Password)

#Import PowerShell Modules  
import-module OperationsManager

#Connect to OpsMgr Management Group  
New-SCOMManagementGroupConnection -ComputerName $MS

#&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;  
#OpsMgr Agent Installation  
#&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;

Foreach($Agent in $AgentList)  
{

Install-SCOMAgent -Name $Agent -PrimaryManagementServer (Get-SCOMManagementserver -Name $MS) -ActionAccount $InstallAccount  
write-host $Agent "Installed"

}

#&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
#Sleep so the agent install can finish before enabling agent proxying  
#&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

Start-Sleep -s 60

#&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
#enabling agent proxying for vmm and AD management pack  
#&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

#Enable Agent Proxying  
Get-ScomAgent | where{$_.ProxyingEnabled.Value -eq $False} | Enable-SCOMAgentProxy  
}

[/xml]

thanks,

Alexandre Verkinderen
