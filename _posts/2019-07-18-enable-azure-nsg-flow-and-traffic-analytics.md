---
title: Enable Azure NSG Flow and Traffic Analytics
date: 2019-07-18T14:24:35+10:00
author: alexandre@verkinderen.com
categories:
  - Azure
  - Powershell
tags:
  - Azure
  - network watcher
  - powershell
---
A while back I wrote a [blog post](https://mscloud.be/enabling-azure-network-security-group-nsg-flow-logging-in-bulk/) on how to enable NSG flow and traffic analytics in bulk for all your NSGs. 

A few things have changed since then so I decided to create a V2 version of the PowerShell script. 



You will notice that the script has been updated to use the new AZ PowerShell modules.  
  
Also we are now enabling [NSG Flow V2](https://azure.microsoft.com/en-au/updates/nsgflowlogsversion2/) instead of V1 which was not available back in 2017 when I wrote the first script.  
To enable v2 the [documentation](https://docs.microsoft.com/en-us/powershell/module/az.network/set-aznetworkwatcherconfigflowlog?view=azps-2.4.0) is saying you should just use &#8221; -FormatVersion 2 &#8220;. However if you do this it will not work. The -formatversion is not passed through the RestAPI. The solution is to specify the format type as well with &#8221; -FormatType Json &#8220;.

Hope this helps,

Alex
