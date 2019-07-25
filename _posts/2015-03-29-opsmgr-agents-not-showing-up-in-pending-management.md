---
id: 8451
title: OpsMgr agents not showing up in pending management
date: 2015-03-29T07:49:17+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=8451
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
  - "8195"
  - "8195"
  - "8195"
image: /wp-content/uploads/2015/03/scom2012-2-150x150.png
categories:
  - Powershell
  - SystemCenter
tags:
  - Operations Manager 2012
  - opsmgr
  - opsmgr 2012
---
Hi,

It has been a long time since I worked with OpsMgr but I encountered a rather strange issue lately. Some manually installed agents sitting behind a Gateway were not showing up in pending management state so I couldn&#8217;t approve them, but other agents were fine.  I even enabled &#8220;automatically approve new manually installed agents&#8221; for a while, reinstalled the agent but still nothing.

[<img class="alignnone  wp-image-8481" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/03/scom.png" alt="OpsMgr agent approval" width="540" height="456" srcset="/wp-content/uploads/2015/03/scom.png 1013w, /wp-content/uploads/2015/03/scom-300x253.png 300w, /wp-content/uploads/2015/03/scom-768x648.png 768w" sizes="(max-width: 540px) 100vw, 540px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/03/scom.png)

As some agents were reporting correctly and showing up immediately in pending management I had a look in the OpsMgr database. You can check which agents are in pending management with this SQL query (run on OperationsManager database). To view the database information on pending actions:

[xml]  
select * from agentpendingaction  
[/xml]

[<img class="alignnone size-full wp-image-8491" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/03/opsmgrdb.png" alt="opsmgrdb agent pending database" width="598" height="213" srcset="/wp-content/uploads/2015/03/opsmgrdb.png 598w, /wp-content/uploads/2015/03/opsmgrdb-300x107.png 300w" sizes="(max-width: 598px) 100vw, 598px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/03/opsmgrdb.png)

You can do the same with PowerShell. Open a command shell, and run the following:

[xml]Get-SCOMPendingManagement  
[/xml]

[<img class="alignnone size-medium wp-image-8561" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/03/opsmgrpowershellagent-300x189.png" alt="opsmgr powershell agent Get-SCOMPendingManagement" width="300" height="189" srcset="/wp-content/uploads/2015/03/opsmgrpowershellagent-300x189.png 300w, /wp-content/uploads/2015/03/opsmgrpowershellagent-768x484.png 768w, /wp-content/uploads/2015/03/opsmgrpowershellagent.png 821w" sizes="(max-width: 300px) 100vw, 300px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/03/opsmgrpowershellagent.png)

To see a prettier view:

[xml]  
Get-SCOMPendingManagement | ft agentname,agentpendingactiontype [/xml]

Now that we could see all our pending agents, you can approval them with Powershell with the  &#8211;**Approve-SCOMPendingManagement**  switch.

To approve them all

[xml]  
Get-SCOMPendingManagement | Approve-SCOMPendingManagement  
[/xml]

To approve specific agent

[xml]  
Get-SCOMPendingManagement | where {$_.AgentName -eq "ServernameFQDN"} | Approve-SCOMPendingManagement  
[/xml]

&nbsp;

So once this worked I investigated a bit more to found out the root cause of this issue. It seemed that the agents that were stuck in agent pending state in the database had been installed before the final Gateway configuration was done to allow the gateway to act as proxy server. One final step for the gateway server is to configure it as a Proxy. In the Operations Console go to the Administration ****space, then click on Management Servers then find the gateway box you just added, Double Click on it. In the Management Server Properties Click the Security tab. Check the box Allow this server to act as a proxy

[<img class="alignnone size-medium wp-image-8581" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/03/opsgrproxy-293x300.png" alt="OpsMgr gateway proxy" width="293" height="300" srcset="/wp-content/uploads/2015/03/opsgrproxy-293x300.png 293w, /wp-content/uploads/2015/03/opsgrproxy-55x55.png 55w, /wp-content/uploads/2015/03/opsgrproxy.png 683w" sizes="(max-width: 293px) 100vw, 293px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/03/opsgrproxy.png)

Hope this helps,  
Alex
