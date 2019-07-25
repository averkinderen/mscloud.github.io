---
id: 684
title: Installing hyper-v inside a vm on Windows Server 2012
date: 2013-03-19T16:07:13+10:00
author: alexandre@verkinderen.com

guid: http://scug.be/scom/?p=684
sc_member_order:
  - "0"
post_views_count:
  - "2189"
  - "2189"
  - "2189"
  - "2189"
categories:
  - Uncategorized
tags:
  - Hyper-V
  - hyperv
  - powershell
  - windows 2008 R2
  - windows 2012
---
&#160;

For a test setup I needed to install a Hyperv inside a vm running Windows server 2012. I did some googling and found the following post <http://www.aidanfinn.com/?p=10175> from Aidan saying that its possible on Win 2008.

So I wanted to give it a try but it failed saying that a Hypervisor was already running

&#160;

[<img title="image" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="image" src="http://www.mscloud.be/wp-content/uploads/2013/03/image_thumb.png" width="244" height="169" />](http://www.mscloud.be/wp-content/uploads/2013/03/image.png) 

Apparently in Windows 2012 Microsoft wont let you install the Hyper-V role inside a VM. Bummer!

So I gave it another try using Powershell and hoping to bypass the validation check by using the following command: “Install-WindowsFeature –Name Hyper-V -ComputerName hyperv01-IncludeManagementTools –Restart” but it failed as well, with same error!

The only solution was to ping my good friend Mike Resseler who told me to try the following powershell command: 

**“DISM /Online /Enable-Feature /FeatureName:Microsoft-Hyper-V"** which let me install Hyperv just fine!

[<img title="image" style="border-top: 0px; border-right: 0px; border-bottom: 0px; border-left: 0px; display: inline" border="0" alt="image" src="http://www.mscloud.be/wp-content/uploads/2013/03/image_thumb1.png" width="244" height="100" />](http://www.mscloud.be/wp-content/uploads/2013/03/image11.png) 

and the following will enable the Hyperv Management console: “**DISM /Online /Enable-Feature /FeatureName:Microsoft-Hyper-V-Management-Clients**”

Thanks,

Alex
