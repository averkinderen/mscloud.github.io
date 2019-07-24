---
id: 7831
title: Create VMM Clouds in bulk with PowerShell
date: 2015-04-21T20:14:41+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://www.mscloud.be/?p=7831
permalink: /create-vmm-clouds-in-bulk-with-powershell/
sc_member_order:
  - "0"
bpxl_standard_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_standard_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_image_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_image_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_audio_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_audio_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_video_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_video_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_link_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_link_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_gallery_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_gallery_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_status_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_status_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_singlerelated:
  - "0"
  - "0"
  - "0"
post_views_count:
  - "3738"
  - "3738"
  - "3738"
categories:
  - Powershell
  - SystemCenter
  - WAP
tags:
  - powershell
  - SCVMM
  - system center
  - VMM
  - WAP
---
As you might remember from my [previous blog post](http://www.mscloud.be/create-virtual-networks-in-vmm-with-powershell/) I&#8217;m working now on a Hyper-V migration project where I couldn&#8217;t reuse the old VMM server. So besides re-creating virtual networks in bulk with Powershell I also had to re-create the clouds defined in the old VMM in bulk with powershell.

The idea is the following:

  1. Export all Clouds from the old VMM to a csv file
  2. Import all cloud to the new VMM from the csv file

So first of all we need to export our Clouds to a CSV by running the following Powershell Commandlet:

[xml]  
Get-SCCloud |Export-Csv -Path C:\Temp\cloud.csv  
[/xml]

&nbsp;

[<img class="alignnone wp-image-8651 size-large" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/03/getclousd-1024x150.png" alt="Get cloud to csv" width="768" height="113" srcset="/wp-content/uploads/2015/03/getclousd-1024x150.png 1024w, /wp-content/uploads/2015/03/getclousd-300x44.png 300w, /wp-content/uploads/2015/03/getclousd-768x113.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/03/getclousd.png)

Now that we have the CSV file we can use it in our new environment to automatically create in bulk the same Clouds.

You can download the <a href="https://gallery.technet.microsoft.com/Create-VMM-Clouds-in-bulk-daa75f49" target="_blank">script here</a>.

The script will read through the CSV, get all the names and create new clouds based on the settings you define in the script like: capacity, hostgroup, virtual network, storage, etc:

[xml]  
#Variables

$CloudCSV = IMPORT-CSV C:\Tmp\Cloud.csv

$CloudDescription = &#8221;  
$hostGroups = @()  
$HostGroups = Get-SCVMHostGroup -Name "All hosts"  
$resources = @()  
$LogicalNetwName = Get-SCLogicalNetwork -Name "Contoso &#8211; Reference &#8211; Network"  
$Storage = Get-SCStorageClassification -Name "Remote Storage"  
$resources += $LogicalNetwName  
$readonlyLibraryShares = @()  
$readonlyLibraryShares += Get-SCLibraryShare | where {$_.Name -match "VMLibrary"}

#Loop through all the clouds in the CSV and create a new cloud for each line  
Foreach ($Cloud in $CloudCSV){

$CloudName = $($Cloud.Name)  
#Create a new job guid per cloud  
$Guid = [System.Guid]::NewGuid()  
Set-SCCloud -JobGroup $Guid  
Set-SCCloudCapacity -JobGroup $Guid -UseCustomQuotaCountMaximum $true -UseMemoryMBMaximum $true -UseCPUCountMaximum $true -UseStorageGBMaximum $true -UseVMCountMaximum $true

$resources += Get-SCPortClassification -Name "Guest Dynamic IP"  
$resources += Get-SCPortClassification -Name "High bandwidth"  
$resources += Get-SCPortClassification -Name "Low bandwidth"

$resources += $Storage

Set-SCCloud -JobGroup $Guid -RunAsynchronously -AddCloudResource $resources -AddReadOnlyLibraryShare $readonlyLibraryShares

New-SCCloud -JobGroup $Guid -VMHostGroup $hostGroups -Name $CloudName -Description $CloudDescription -RunAsynchronously  
}

[/xml]

Hope this helps,  
Alex