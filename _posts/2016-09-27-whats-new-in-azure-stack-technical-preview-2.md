---
id: 13321
title: What’s new in Azure Stack Technical Preview 2
date: 2016-09-27T01:46:32+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=13321
sc_member_order:
  - "0"
  - "0"
  - "0"
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
  - "2284"
  - "2284"
  - "2284"
image: /wp-content/uploads/2016/09/azurestack-150x150.png
categories:
  - Azure
tags:
  - Azure
  - azure stack
  - cubesys
---
Azure Stack Technical Preview 2 has just been released at Ignite!! This release provides new features for both tenants and administrators.

[<img class="alignnone size-medium wp-image-13371" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/azurestack-300x168.png" alt="azurestack" width="300" height="168" srcset="/wp-content/uploads/2016/09/azurestack-300x168.png 300w, /wp-content/uploads/2016/09/azurestack-768x429.png 768w, /wp-content/uploads/2016/09/azurestack.png 965w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/azurestack.png)

Have a look at the new features:

## Key vault

  * Key Vault provides secure management of your keys and passwords for cloud apps. Allows for auditing and monitoring of key usage by apps and VMs.

## Network

  * iDNS provides internal network name registration and DNS resolution without additional DNS infrastructure.
  * Virtual Network Gateways provide VPN connectivity options to Azure or other on-premises resources.
  * User Defined Routes allow you to route network traffic through firewall, security, or other appliances and services.
  * You can create network resources from the marketplace

##  Storage

  * Azure Queues enable reliable and persistent service messaging
  * Storage analytics capture storage performance data. You can use this data to trace requests, analyze usage trends, and diagnose issues with your storage account
  * Storage service support for common tools and SDKs, such as Azure CLI, PowerShell, .NET, Python, and Java SDK
  * Storage Account Shared Access Signature enable granular delegation of access to your storage services without having to share your full account key.
  * Storage services now use Group Managed Service Accounts for strong security with low management overhead

##  VMs and Resource Manager

  * You can deallocate and capture virtual machines, redeploy virtual machine extensions, and resize virtual machine disks.
  * Export Resource Manager templates from portal. Billing and usage
  * Billing and consumption APIs expose data on how your services are consumed.
  * You can capture plans and offers in Resource Manager templates.
  * Delegated Providers enable resellers to offer your Azure Stack services to their customers.
  * Reclaim unused tenant resources on-demand.

## Monitoring and health

  * Azure Stack Regions are a logical unit of scale and management within Azure Stack. In this preview, you can view resource consumption of network, storage, and compute resources by region.
  * New monitoring capabilities available in the portal and APIs allow you to proactively view and manage alerts on your environment.
  * System Health Tests automatically test your fabric to ensure services are working as expected

More info can be found here: https://azure.microsoft.com/en-us/documentation/articles/azure-stack-architecture/

Thank you,

Alexandre Verkinderen
