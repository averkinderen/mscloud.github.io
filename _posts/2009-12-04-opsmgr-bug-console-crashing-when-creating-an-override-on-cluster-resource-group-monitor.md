---
id: 2411
title: 'OpsMgr bug : console crashing when creating an override on cluster resource group monitor'
date: 2009-12-04T12:59:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2009/12/04/opsmgr-bug-console-crashing-when-creating-an-override-on-cluster-resource-group-monitor.aspx
permalink: /opsmgr-bug-console-crashing-when-creating-an-override-on-cluster-resource-group-monitor/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1965"
  - "1965"
  - "1965"
  - "1965"
  - "1965"
  - "1965"
  - "1965"
  - "1965"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - bug
  - cluster
  - Issue
  - Management Pack
  - Operations Manager 2007
  - Opmsgr 2007 R2
  - opsmgr R2
---
Be aware that there is a bug when you want to create an override on the resource group rollup monitor to change the maintenance mode behavior!

[<img height="114" width="114" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/big_ugly_bug_thumb_0C20F8C4.png" alt="big_ugly_bug" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/big_ugly_bug_1A5F71B4.png)

Let&rsquo;s see:

In my example I have one cluster with 2 cluster nodes. I needed to do some maintenance on my nodes and they needed to be rebooted. So I put one node in maintenance mode so that my NOC team will not get alerted, do what I had to do and finally restarted my node and do the same for the other node.

&nbsp;

Suddenly I had someone of the NOC team yelling at me that they did receive an alert saying that there was a problem with the cluster resource group!!

&nbsp;

I opened the cluster resource group health explorer and indeed:

[<img height="151" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_4E939AFA.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_19F33EBF.png)

The underlying resources were in maintenance mode but not the availability rollup monitor! So I had a look at the monitor and apparently the monitor is configured to rollup maintenance mode as an error:

&nbsp;

[<img height="179" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_7C14BABD.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_60702EC7.png)

So I wanted to change the maintenance mode parameter so that when I put a node into maintenance mode the monitor will rollup the maintenance mode as maintenance&nbsp; mode and not rollup the maintenance mode as an error:

[<img height="131" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_7BA887C8.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_22E2D0FE.png)

And here is the catch:

[<img height="155" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_77320701.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_5063F0C1.png)

&nbsp;

When you want to save your override you will get this nice red error! So it&rsquo;s impossible to change how the behavior of the rollup resource group monitor!

&nbsp;

So now, when we need to put a cluster node in maintenance mode we also put the resource groups in maintenance mode.

&nbsp;

Have fun,

Alexandre Verkinderen
