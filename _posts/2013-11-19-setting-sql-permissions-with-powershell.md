---
id: 706
title: Setting SQL permissions with Powershell
date: 2013-11-19T00:08:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://scug.be/scom/?p=706
permalink: /setting-sql-permissions-with-powershell/
sc_member_order:
  - "0"
post_views_count:
  - "1762"
  - "1762"
  - "1762"
  - "1762"
categories:
  - SystemCenter
tags:
  - powershell
  - sql
  - system center
---
&nbsp;

In the next couple of posts I’m going to blog about automating a System Center post-configuration deployment with Powershell. After you have deployed a typical SC environment you still need to do quite a lot of configuration. The following posts will cover how to automate this with Powershell.

&nbsp;

The first powershell script is to define a specific user account as a sysadmin on a bunch of SQL servers:

[powershell]

<sub>#Variables  
$Servers = @("srv01.contoso.com",”srv02.contoso.com”)</sub>

<sub>  
#Connect remotely to the server</sub>

<sub>  
Foreach($Server in $Servers)  
{ </sub>

<sub>Invoke-Command -ComputerName $Server -ScriptBlock { </sub>

<sub>  
#Set the system account as sysadmin</sub>

<sub>[System.Reflection.Assembly]::LoadWithPartialName(&#8216;Microsoft.SqlServer.SMO&#8217;) | out-null </sub>

<sub># Create SMO Connections to both SQL Instances  
$Svr = New-Object (&#8216;Microsoft.SqlServer.Management.Smo.Server&#8217;) "$server"  
$svrole = $svr.Roles | where {$_.Name -eq &#8216;sysadmin&#8217;}  
$svrole.AddMember("User account”)  
}  
}</sub>

[/powershell]

Thanks,

Alex