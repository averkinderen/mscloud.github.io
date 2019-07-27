---
id: 19551
title: Enabling Azure Network Security Group (NSG) flow logging in bulk
date: 2017-06-06T16:04:57+10:00
author: alexandre@verkinderen.com
guid: http://www.mscloud.be/?p=19551
sc_member_order:
  - "0"
  - "0"
  - "0"
post_views_count:
  - "6606"
  - "6606"
  - "6606"
  - "6606"
image: /wp-content/uploads/2017/05/network_watcher-150x150.png
categories:
  - Azure
tags:
  - Azure
  - network watcher
  - NSG
  - powershell
---
<span lang="EN-AU">As we speak one of my customers is looking into using Azure Network Watcher for its network auditing and packet logging capabilities. </span><span lang="EN-AU">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group. </span><span lang="EN-AU">While flow logs target Network Security Groups, they are not displayed in the same way as the other logs. Flow logs are stored only within a storage account.</span>

## <span lang="EN-AU">The Challenge:</span>

<span lang="EN-AU">The big challenge to enable NSG flow logging is that you have to do it one by one in the Azure portal. A step-by-step guide on how to do this is described <a href="https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-portal">here</a>.  You need to select the NSG, tick the box to enable NSG flow logging, specify a storage account etc. This is going to take ages to enable for all my NSG&#8217;s! For my customer, this wasn’t going to work as they have a lot of NSG’s defined in their environment.</span>

<span lang="EN-AU">This blog post will cover how you can enable NSG flow logs for all your NSG’s at once with a PowerShell Script.</span>

## Before you begin {#before-you-begin}

<p class="lf-text-block lf-block" data-lf-anchor-id="9da02eb9a5e230a891c99d464f610341:0">
  This scenario assumes you have already followed the steps in <a href="https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-create" data-linktype="relative-path">Create a Network Watcher</a> to create a Network Watcher. The scenario also assumes that a Resource Group with a storage account has been pre-created.
</p>

## <span lang="EN-AU">Solution:</span>

The following PowerShell script will enable NSG Flow logging for all my NSG&#8217;s. The script will do the following:

* Ask for a Resource Group that will be used for saving the NSG logs
  * Ask for a storage account that will be used for saving logs
  * You need to specify the retention period of the NGS logs
  * Ask for a subscription in which you want to enable NSG flow logging
  * In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered. The script will register the provider.

NSG flow logging needs to be enabled per Azure Region and per subscription, so the script will loop through all the different regions where Network watcher is enabled. If the script finds an NSG in that region, it will enable NSG flow logging

[<img class="alignnone size-large wp-image-19571" src="http://www.mscloud.be/wp-content/uploads/2017/05/enablensgflow1-1024x529.png" alt="" width="768" height="397" srcset="/wp-content/uploads/2017/05/enablensgflow1-1024x529.png 1024w, /wp-content/uploads/2017/05/enablensgflow1-300x155.png 300w, /wp-content/uploads/2017/05/enablensgflow1-768x397.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](http://www.mscloud.be/wp-content/uploads/2017/05/enablensgflow1.png)

Once we find a region where Network Watcher is enabled, we will look for NSGs and enable flow logging:

[<img class="alignnone size-large wp-image-19661" src="http://www.mscloud.be/wp-content/uploads/2017/05/enableflowbluredpng-1024x433.png" alt="" width="768" height="325" srcset="/wp-content/uploads/2017/05/enableflowbluredpng-1024x433.png 1024w, /wp-content/uploads/2017/05/enableflowbluredpng-300x127.png 300w, /wp-content/uploads/2017/05/enableflowbluredpng-768x324.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](http://www.mscloud.be/wp-content/uploads/2017/05/enableflowbluredpng.png)

&nbsp;

That&#8217;s it! We just enabled NSG flow logging with one press of a button! You can find the PowerShell script below:

<div class="oembed-gist">
  <noscript>
    View the code on <a href="https://gist.github.com/averkinderen/3d03a0d5e2231e8cf97b5ba0e6cae08e">Gist</a>.
  </noscript>
</div>

In the next blogpost I will cover how to visualize this data with PowerBi.

Hope this helps,

Alexandre Verkinderen
