---
id: 19876
title: Move Managed Disks to another subscription
date: 2018-10-23T11:26:10+10:00
author: alexandre@verkinderen.com
guid: http://mscloud.be/?p=19876
sc_member_order:
  - "0"
bpxl_standard_excerpt_home:
  - "0"
bpxl_standard_single_hide:
  - "0"
bpxl_image_excerpt_home:
  - "0"
bpxl_image_single_hide:
  - "0"
bpxl_audio_excerpt_home:
  - "0"
bpxl_audio_single_hide:
  - "0"
bpxl_video_excerpt_home:
  - "0"
bpxl_video_single_hide:
  - "0"
bpxl_link_excerpt_home:
  - "0"
bpxl_link_single_hide:
  - "0"
bpxl_gallery_excerpt_home:
  - "0"
bpxl_gallery_single_hide:
  - "0"
bpxl_status_excerpt_home:
  - "0"
bpxl_status_single_hide:
  - "0"
bpxl_singlerelated:
  - "0"
post_views_count:
  - "1468"
categories:
  - Azure
tags:
  - Azure
  - Azure Disk
  - cli
  - Cloud
  - Disk
---
It is strongly recommended to use managed disks when deploying virtual machines in Azure. But one of the downsides of managed disks is that you are unable to move your virtual machines to another subscription. That is&#8230;.until now!

At Ignite 2018 Microsoft announced an update to the Microsoft.Compute Resource provider that let&#8217;s us move virtual machines with managed disks. To be able to use the new feature you need to register the new Resource Provider feature first with the following command from PowerShell or from the Azure CLI.

First open the Azure CLI from the Azure portal

[<img class="alignnone size-medium wp-image-19886" src="/wp-content/uploads/2018/10/cli-300x161.png" alt="" width="300" height="161" srcset="/wp-content/uploads/2018/10/cli-300x161.png 300w, /wp-content/uploads/2018/10/cli-768x411.png 768w, /wp-content/uploads/2018/10/cli-1024x548.png 1024w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/10/cli.png)

and run the following command:

[<img class="alignnone size-medium wp-image-19895" src="/wp-content/uploads/2018/10/feature-1-300x96.png" alt="" width="300" height="96" srcset="/wp-content/uploads/2018/10/feature-1-300x96.png 300w, /wp-content/uploads/2018/10/feature-1-768x245.png 768w, /wp-content/uploads/2018/10/feature-1-1024x327.png 1024w, /wp-content/uploads/2018/10/feature-1.png 1330w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/10/feature-1.png)

&nbsp;

<pre class="lang:ps decode:true ">az feature register --namespace Microsoft.Compute --name ManagedResourcesMove</pre>

Once the feature &#8220;ManagedResourcesMove&#8221; is registered you need to invoke the Resource Provider registration to propagate the change.

[<img class="alignnone size-medium wp-image-19888" src="/wp-content/uploads/2018/10/provider-300x211.png" alt="" width="300" height="211" srcset="/wp-content/uploads/2018/10/provider-300x211.png 300w, /wp-content/uploads/2018/10/provider.png 625w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/10/provider.png)

<pre class="lang:ps decode:true ">az provider register --namespace Microsoft.Compute</pre>

It can take quite some time for the updated Resource Provider to be propagated. You can monitor the status with

<pre class="lang:ps decode:true ">az provider show -n Microsoft.Compute</pre>

After a few minutes you should be able to move your virtual machine to another subscription!

[<img class="alignnone size-medium wp-image-19890" src="/wp-content/uploads/2018/10/move-300x153.png" alt="" width="300" height="153" srcset="/wp-content/uploads/2018/10/move-300x153.png 300w, /wp-content/uploads/2018/10/move-768x393.png 768w, /wp-content/uploads/2018/10/move-1024x524.png 1024w, /wp-content/uploads/2018/10/move.png 1148w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/10/move.png)

[<img class="alignnone size-medium wp-image-19892" src="/wp-content/uploads/2018/10/success-300x75.png" alt="" width="300" height="75" srcset="/wp-content/uploads/2018/10/success-300x75.png 300w, /wp-content/uploads/2018/10/success.png 527w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/10/success.png)

Thanks,  
Alex
