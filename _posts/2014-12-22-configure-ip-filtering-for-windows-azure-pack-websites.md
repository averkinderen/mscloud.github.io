---
id: 4461
title: Configure IP filtering for Windows Azure Pack Websites
date: 2014-12-22T13:12:02+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=4461
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
  - "3210"
  - "3210"
  - "3210"
categories:
  - WAP
tags:
  - powershell
  - WAP
  - websites
---
Setting an IP filter is very important because one of the easiest ways to launch a denial of service (DoS) attack is to launch the attack from inside the service itself. Therefore, at minimum, the hosting service provider should blacklist the farm from itself.

For example, if the web farm is deployed to a subnet, then the subnet IP addresses should be filtered to prevent web sites from calling back into the farm and launching (for example) a DoS attack.

To restrict tenant worker processes from accessing the IP address ranges corresponding to servers inside the Web Site cloud, you can configure IP filtering either in the Windows Azure Pack management portal or by using PowerShell.

To configure IP filtering in the Management Portal for Administrators, perform the following steps:

  1. In the left pane of the portal, choose Web Site Clouds.</p> 
  2. Select the web site cloud that you want to configure.

  3. Choose Block List.

  4. In the command bar at the bottom of the portal, choose Add.

  5. In the Enter an IP Address Range dialog, enter an IP address in the Start Address and End Address boxes to create the range.

[<img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px; display: inline; padding-right: 0px; border: 0px;" title="image" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2014/12/image_thumb1.png" alt="image" width="244" height="185" border="0" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2014/12/image1.png)

  1. Click the check mark to complete the operation.

To configure IP filtering by using PowerShell, run the following PowerShell cmdlets on the controller. Replace <start-of-ip-blacklist-range> and <end-of-ip-blacklist-range> with valid IP addresses.

[xml]

Add-pssnapin WebHostingSnapin

Set-Hostingconfiguration -WorkerRegKeyRejectPrivateAddresses 1

Set-Hostingconfiguration –WorkerRegKeyPrivateAddressRange “192.168.0.10”, ‘192.168.0.100’  
[/xml]

&nbsp;

Finally, restart the Dynamic WAS Service (DWASSVC) on servers configured to run the web worker role. Run the following commands from an elevated command prompt:

[xml]

net stop dwassvc

net start dwassvc  
[/xml]

&nbsp;

Thanks,

Alex
