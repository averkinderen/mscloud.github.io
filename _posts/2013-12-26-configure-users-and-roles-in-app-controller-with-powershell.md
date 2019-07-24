---
id: 733
title: Configure users and Roles in App Controller with Powershell
date: 2013-12-26T12:41:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://scug.be/scom/?p=733
permalink: /configure-users-and-roles-in-app-controller-with-powershell/
sc_member_order:
  - "0"
post_views_count:
  - "1601"
  - "1601"
  - "1601"
  - "1601"
categories:
  - Powershell
  - SystemCenter
tags:
  - app controller
  - powershell
  - system center
---
I had to configure remotely some users and Roles in App controller with Powershell.  You can find a lot of all App Controller CMDLets here <http://technet.microsoft.com/en-us/library/jj899760(v=sc.20).aspx>.

Below you can find the Powershell Script used to connect remotely to the app controller server and add users to the appropriate User Roles:

[xml]

#=======================================================================  
#  
\# NAME: Configure App Controller  
#  
\# AUTHOR: Alexandre Verkinderen  
\# DATE  : 10/29/2013  
#  
\# Requirements:  
#  
\# COMMENT:  
#=======================================================================

#Variables  
$APPC = "SCVMM01.contoso.com"

Invoke-Command -ComputerName $APPC -ScriptBlock {

#import App Controller module  
Import-Module -Name AppController

#Variables  
$APPC = "<a href="https://scvmm01.contoso.com&quot;">https://scvmm01.contoso.com"</a>  
$User1 = "contosodeveloper"  
$User2 = "contosoendsuer"  
$Password = ConvertTo-SecureString "Passw0rd!" -AsPlainText -Force  
$username = "contosoadministrator"  
$Credentials = New-Object System.Management.Automation.PSCredential($username,$Password)

#Connect to App Controller  
Get-SCACServer -ServerName $APPC -Credential $Credentials

#Retrieve Userroles  
$UserRole = Get-SCACUserRole –Managed | where { $_.Name –eq "Administrators" }

#Add users to Administrator User Role

Set-SCACUserRole -UserRole $UserRole -AddMembers $User1,$User2  
Write-Host $User1 " and " $User2 " added to App Controller" -foregroundcolor green

}

[/xml]