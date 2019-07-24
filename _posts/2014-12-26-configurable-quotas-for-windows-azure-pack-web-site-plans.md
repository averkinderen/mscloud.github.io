---
id: 4561
title: Configurable Quotas for Windows Azure Pack Web Site Plans
date: 2014-12-26T13:30:29+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://www.mscloud.be/?p=4561
permalink: /configurable-quotas-for-windows-azure-pack-web-site-plans/
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
  - "3105"
  - "3105"
  - "3105"
categories:
  - WAP
tags:
  - quota
  - WAP
  - websites
---
After setting up Windows Azure Pack Web Sites, you can create sets of offerings (or “plans”) for the tenant customers who will use your web site hosting service.

<img class="" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2014/12/image1-1024x522.png" alt="" width="606" height="309" />  
You can create as many plans as you want and name them as you wish. Each plan that you create will have three levels of service: Intro (Shared), Basic (Shared), and Reserved. For each of the three levels, you can configure 17 different quotas related to web site features and capacities.

<img class="" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2014/12/image1-1024x672.png" alt="" width="710" height="466" /> 

The combination of quotas that you set for each level of service determines the restrictions and benefits that each level of service in the plan will have.

&nbsp;

<table border="1" cellspacing="0" cellpadding="0">
  <tr>
    <td valign="top" width="369">
      <b>Quota Name</b>
    </td>
    
    <td valign="top" width="369">
      <b>Description</b>
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Subscription CPU Time
    </td>
    
    <td valign="top" width="369">
      Represents, in minutes, the CPU time a subscription&#8217;s websites can consume across all instances over a specified enforcement period. You can specify a value or choose the Unlimited option. The default for each service level is Unlimited. There is an Enforcement Duration (Minutes) setting, for which the default is 1440 (=24 hours). The Exceed Action setting is available.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Subscription CPU Burst Time
    </td>
    
    <td valign="top" width="369">
      Represents, in minutes, the CPU time a subscription&#8217;s websites can consume across all instances over a specified enforcement period. A shorter enforcement duration can help reduce CPU spikes. You can specify a value or choose the Unlimited option. The default for each service level is Unlimited. The default Enforcement Duration (Minutes) setting is 1440 (=24 hours). The Exceed Action setting is available.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Process CPU Burst %
    </td>
    
    <td valign="top" width="369">
      Represents the CPU percentage a worker process can consume over a specified enforcement period. The default for each service level is 100 percent. The default Enforcement Duration (Minutes) setting is 10 minutes.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Subscription Memory – Maximum Working Set
    </td>
    
    <td valign="top" width="369">
      Represents, in megabytes, the physical memory (RAM) a subscription&#8217;s websites can consume over a specified enforcement duration. You can specify a value in megabytes or choose the Unlimited option. The default for each service level is Unlimited. The default Enforcement Duration (Minutes) setting is 1440 (=24 hours). The Exceed Action setting is available.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Process Memory Limit
    </td>
    
    <td valign="top" width="369">
      Represents the total memory a worker process can consume. The default for each service level is 1024 (=1 gigabyte).
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Process Memory – Maximum Working Set
    </td>
    
    <td valign="top" width="369">
      Represents, in megabytes, the physical memory (RAM) a worker process can consume. The default for each service level is 1024 (=1 gigabyte).
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Subscription Bytes In
    </td>
    
    <td valign="top" width="369">
      Represents, in megabytes, the incoming bandwidth a subscription&#8217;s websites can consume over a specified enforcement period. You can specify a value in megabytes or choose the Unlimited option. The default for each service level is Unlimited. The default Enforcement Duration (Minutes) setting is 1440 (=24 hours). The Exceed Action setting is available.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Subscription Bytes Out
    </td>
    
    <td valign="top" width="369">
      Represents, in megabytes, the outgoing bandwidth a subscription&#8217;s websites can consume over a specified enforcement period. You can specify a value in megabytes or choose the Unlimited option. The default for each service level is Unlimited. The default Enforcement Duration (Minutes) setting is 1440 (=24 hours). The Exceed Action setting is available.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Subscription Storage Space
    </td>
    
    <td valign="top" width="369">
      Represents, in megabytes, the storage space a subscription&#8217;s websites can consume. You can specify a value in megabytes or choose the Unlimited option. The Shared setting configures both the Intro (Shared) and Basic (Shared) service levels. There is a separate setting for Reserved. The default for each service level is 1024 (=1 gigabyte).
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Subscription Site Count
    </td>
    
    <td valign="top" width="369">
      Represents the number of websites in a subscription. You can specify a number or choose the Unlimited option. Unlimited is the default for each service level.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Subscription Web Worker Count
    </td>
    
    <td valign="top" width="369">
      Represents the number of web workers a subscription&#8217;s websites can consume simultaneously. You can specify a number or choose the Unlimited option. Unlimited is the default for each service level.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Subscription Custom Domain Support
    </td>
    
    <td valign="top" width="369">
      Enables or disables custom domain names. Off is the default setting for Intro (Shared). On is the default setting for Basic (Shared) and Reserved.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Subscription SSL Support
    </td>
    
    <td valign="top" width="369">
      Enables or disables custom SSL certificates. Possible values are Off, SNI, SNI and IPv4, SNI and IPv6, and SNI, IPv4 and IPv6. The default for Intro (Shared) is Off. The default for Basic (Shared) is SNI. The default for Reserved is SNI and IPv4.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Subscription 64 bit Worker Process Support
    </td>
    
    <td valign="top" width="369">
      Enables or disables 64 bit worker processes. Off is the default for Intro (Shared) and Basic (Shared). On is the default for Reserved.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Subscription WebSocket Support
    </td>
    
    <td valign="top" width="369">
      Enables or disables the WebSocket protocol. Off is the default for Intro (Shared) and Basic (Shared). On is the default for Reserved.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Process Concurrent Request Limit
    </td>
    
    <td valign="top" width="369">
      Represents the number of concurrent requests permitted per worker process. You can specify the number of connections. The default is 5000 for each service level.
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="369">
      Process Idle Timeout
    </td>
    
    <td valign="top" width="369">
      Represents, in minutes, the amount of time that a worker process is allowed to remain idle before it is stopped. The default for Intro (Shared) is 20 minutes. The default for Basic (Shared) is 60 minutes. The default for Reserved is 10080 (=7 days).
    </td>
  </tr>
</table>

Click the name of a quota to select it, and then choose Edit in the command bar at the bottom of the page to edit it. In the Quota dialog, specify the values that you want to enforce for each service level. Notice that:

  * Some quotas have an Enforcement Duration (Minutes) setting.
  * Some quotas have an Exceed Action  setting, for which the options are Do nothing, Stop web site, or Redirect to parking page.  
    [<img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2014/12/image_thumb1.png" alt="image" width="181" height="161" border="0" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2014/12/image1.png)

So you can create very customized qouta&#8217;s and plans for the websites with some automatic enforcment like automaticily stopping the website or redirecting it to a parking page.

Thanks,

Alexandre Verkinderen