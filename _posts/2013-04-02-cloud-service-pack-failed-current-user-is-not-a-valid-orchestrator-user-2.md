---
id: 2961
title: 'Cloud Service pack failed: Current user is not a valid Orchestrator user'
date: 2013-04-02T09:46:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://scug.be/scom/?p=696
permalink: /cloud-service-pack-failed-current-user-is-not-a-valid-orchestrator-user-2/
sc_member_order:
  - "0"
post_views_count:
  - "4857"
  - "4857"
  - "4857"
categories:
  - SystemCenter
tags:
  - Cloud
  - Cloud Service pack
  - Orchestrator
  - Service Manager
  - SP1
  - system center
---
Microsoft released beginning of March the updated Cloud Service Process pack that is now fully compatible with System Center 2012 SP1. You can download the new process pack here: [http://www.microsoft.com/en-us/download/details.aspx?id=36497](http://www.microsoft.com/en-us/download/details.aspx?id=36497 "http://www.microsoft.com/en-us/download/details.aspx?id=36497")&#160;&#160; CSPP is an extension pack built on top of System Center. This release is compatible only with System Center 2012 and 2012 SP1. This release does not contain a new feature set from prior releases.

When I tried to install CSPP I got the following error:

[<img title="clip_image001" style="border-left-width: 0px;border-right-width: 0px;border-bottom-width: 0px;border-top-width: 0px" border="0" alt="clip_image001" src="http://www.mscloud.be/wp-content/uploads/2013/03/clip_image001_thumb.png" width="244" height="185" />](http://www.mscloud.be/wp-content/uploads/2013/03/clip_image001.png)

I opened the log files of the CSSP setup that are located at the following location:

C:UsersalexAppDataLocalSCCloudServicesLOGSSCCloudServicesSetupWizard07

When I search through the log file I discovered the following error:

[<img title="clip_image003" style="border-left-width: 0px;border-right-width: 0px;border-bottom-width: 0px;border-top-width: 0px" border="0" alt="clip_image003" src="http://www.mscloud.be/wp-content/uploads/2013/03/clip_image003_thumb.jpg" width="244" height="43" />](http://www.mscloud.be/wp-content/uploads/2013/03/clip_image003.jpg)

03:12:25:Checking if current user is valid Orchestrator user or not  
03:12:27:System.Runtime.InteropServices.COMException (0x800708AC): The group name could not be found.

My account is a local admin and I could perfectly connect to Orchestator and create and launch runbooks so I was quite suprised to see this error.

So I looked locally in computer managed and you need two groups: the first one is the OrchestratorSystemGroup and the second one is the OrchestratorUserGroup which apparently didn’t exist on my orchestrator server! This means the Orchestator pre-requisites checker is checking for a group which doesn’t exist locally!

[<img title="clip_image005" style="border-left-width: 0px;border-right-width: 0px;border-bottom-width: 0px;border-top-width: 0px" border="0" alt="clip_image005" src="http://www.mscloud.be/wp-content/uploads/2013/03/clip_image005_thumb.jpg" width="244" height="217" />](http://www.mscloud.be/wp-content/uploads/2013/03/clip_image005.jpg)

So I created manually a new group and added my account to the group

[<img title="clip_image007" style="border-left-width: 0px;border-right-width: 0px;border-bottom-width: 0px;border-top-width: 0px" border="0" alt="clip_image007" src="http://www.mscloud.be/wp-content/uploads/2013/03/clip_image007_thumb.jpg" width="244" height="240" />](http://www.mscloud.be/wp-content/uploads/2013/03/clip_image007.jpg)

[<img title="clip_image009" style="border-left-width: 0px;border-right-width: 0px;border-bottom-width: 0px;border-top-width: 0px" border="0" alt="clip_image009" src="http://www.mscloud.be/wp-content/uploads/2013/03/clip_image009_thumb.jpg" width="244" height="77" />](http://www.mscloud.be/wp-content/uploads/2013/03/clip_image009.jpg)

After that I closed and re-opened the setup wizard and everything went through without any issues!

Hope this helps,

Alex