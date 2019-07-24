---
id: 19709
title: 'Part 1: Bulk import server locations with PowerShell'
date: 2014-03-24T14:47:02+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://scug.be/scom/?p=776
permalink: /part-1-bulk-import-server-locations-with-powershell/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2321"
  - "2321"
  - "2321"
categories:
  - Powershell
  - SystemCenter
  - Uncategorized
tags:
  - opsmgr
  - powershell
  - system center
  - system center operations manager
---
For a recent project I had to specify the longitude and latitude for all my  servers (about a 1000)  to be able to show them on a map.

In OpsMgr 2012 you can now use the the following new PowerShell CMDlets:

  1. The **New-SCOMLocation** cmdlet creates a location. You can associate agent-managed computers, management servers, or resource pools with a location by using the **Set-SCOMLocation** cmdlet. The Web Application Availability Monitoring Summary Map Dashboard displays the items that you associate with a location.
  2. The **Set-SCOMLocation** cmdlet associates one or more agent-managed computers, management servers, or resource pools with a location. This cmdlet removes a current association, if one exists. The Web Application Availability Monitoring Summary Map Dashboard displays state information for agents, management servers, and resource pools associated with a location.

So In part 1 of this blog series I’m going to create a PowerShell script to bulk import my  locations and then in <a href="http://scug.be/scom/?p=782" target="_blank">part 2 a second script to bulk associate servers to a certain location</a>. Lastly I’m going to utilize all those locations and GPS coordinates in a map.

The following PowerShell script will add the Longitude and Latitude coordinates of about 790 cities from a CSV file. <a href="https://www.dropbox.com/s/6c61mp43mu2sgdx/Locations.csv" target="_blank">You can download the CSV file from here</a>.

[xml]

# //\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***

# // **\*\\*\* Script Header \*\*\***

# //

# // Solution:

# // File:      Addlocations.ps1

# // Author:    Alexandre Verkinderen

# // Purpose:   Add locations from excell

# //

# //

# // **\*\\*\* End Header \*\*\***

# //\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***\***

# //&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

#//  
#//  Global constant and variable declarations  
#/  
#//&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

$list = Import-Csv -Path "C:tempLocations.csv"

$MS = "SCOMSERVER4"

Import-Module OperationsManager  
#Connect to OpsMgr Management GroupStart-OperationsManagerClientShell -ManagementServerName: $MS -PersistConnection: $true -Interactive: $true

#//&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-  
#//  Main routines  
#//&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

foreach ($entry in $list)  
{

$name = $entry.Name  
$Long = $entry.Long  
$Lat = $entry.Lat  
#Set location  
New-SCOMLocation –DisplayName $Name –Latitude $Lat –Longitude $Long

write-host Location $name added

}  
[/xml]

Stay tuned for part 2.

Alexandre Verkinderen