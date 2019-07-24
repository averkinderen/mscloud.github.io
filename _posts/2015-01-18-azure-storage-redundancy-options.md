---
id: 4821
title: Azure Storage Redundancy options
date: 2015-01-18T07:35:44+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://www.mscloud.be/?p=4821
permalink: /azure-storage-redundancy-options/
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
  - "11709"
  - "11709"
  - "11709"
image: /wp-content/uploads/2015/02/StorSimple-150x150.png
categories:
  - Azure
tags:
  - Azure
  - sql
  - Storage
---
Hi,

I was looking into the different Azure Redudancy Storage options and thought it would be a good idea to summarize all the different options in one blogpost. This post is not going to discuss the different storage performance options (like <a href="http://azure.microsoft.com/en-us/documentation/articles/storage-premium-storage-preview-portal/" target="_blank">Premium vs standard storage</a>) for different workloads (like SQL or SharePoint). I might create another blogpost to cover the Azure storage performance options but let&#8217;s focus now on the Redundancy options.

First of all when looking into storage redundancy options the region and location of the dacenter is important. We often refer to the Primary Region and Secondary region as the data gets replicated a few times in the same region and outside the region. So before we deep dive into the different Azure Storage redudancy options let&#8217;s have a look at the different regions Azure is covering as of today:

<img class="" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/azure-regions.png" alt="" width="843" height="592" /> 

> Please note that a region is not necessarily a single location, since there may well be multiple data centers or facilities per region and though they will be “near” each other, this is not necessarily in the same city – they could be 1 kilometer apart with a city border between them.

##  Azure Storage redundancy Options

  *  **Locally Redundant Storage**:  Locally redundant storage maintains three copies of your data. LRS is replicated three times <span style="text-decoration: underline;">within a single facility in a single region</span>. LRS protects your data from normal hardware failures, but not from the failure of a single facility. In this case of Storage A in Datacenter A in Ireland would have a hardware failure your data would still be available on Storage B in Datacenter A in Ireland. But this also means that if datacenter A in Ireland would have a major failure and the Ireland facility would be lost your storage would be lost as well.
  * **Zone Redundant Storage**: ZRS is replicated three times across two to three facilities, either within a single region or across two regions, providing higher durability than LRS. <span style="text-decoration: underline;">ZRS ensures that your data is durable within a single region</span>. This means that if datacenter A in Ireland would be lost your data would still be available in 2 other facilities in the same region.
  * **Read-Access Geographically Redudant Storage**: Read access geo-redundant storage replicates your data to a secondary geographic location, and also provides read access to your data in the secondary location. Read-access geo-redundant storage allows you to access your data from either the primary or the secondary location, in the event that one location becomes unavailable.
  * **Geographically Redundant Storage**: With GRS, your data is r<span style="text-decoration: underline;">eplicated three times within the primary region, and is also replicated three times in a secondary region hundreds of miles away from the primary region</span>, providing the highest level of durability. So you have 6 copies in total. In the event of a failure at the primary region, Azure Storage will failover to the secondary region. GRS ensures that your data is durable in two separate regions. This means that if Ireland would have a blackout all 3 copies in Ireland would be lost but your data would still be available in the Netherlands 3 times.

With GRS, requests to write data are replicated asynchronously to the secondary region. It is important to note that opting for GRS does not impact latency of requests made against the primary region. However, since asychronous replication involves a delay, in the event of a regional disaster it is possible that changes that have not yet been replicated to the secondary region may be lost if the data cannot be recovered from the primary region.  
When you create a storage account, you select the primary region for the account. The secondary region is determined based on the primary region, and cannot be changed. The following map shows the primary and secondary region pairings:

&nbsp;

<table border="1" cellspacing="0" cellpadding="0">
  <tr>
    <td valign="top" width="171">
      <strong>Primary</strong>
    </td>
    
    <td valign="top" width="171">
      <strong>Secondary</strong>
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="171">
      North Central US
    </td>
    
    <td valign="top" width="171">
      South Central US
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="171">
      South Central US
    </td>
    
    <td valign="top" width="171">
      North Central US
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="171">
      East US
    </td>
    
    <td valign="top" width="171">
      West US
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="171">
      West US
    </td>
    
    <td valign="top" width="171">
      East US
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="171">
      North Europe
    </td>
    
    <td valign="top" width="171">
      West Europe
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="171">
      West Europe
    </td>
    
    <td valign="top" width="171">
      North Europe
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="171">
      South East Asia
    </td>
    
    <td valign="top" width="171">
      East Asia
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="171">
      East Asia
    </td>
    
    <td valign="top" width="171">
      South East Asia
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="171">
      East China
    </td>
    
    <td valign="top" width="171">
      North China
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="171">
      North China
    </td>
    
    <td valign="top" width="171">
      East China
    </td>
  </tr>
</table>

&nbsp;

##  Azure Storage redundancy overview

The following table provides you with a summary of the different redudancy options and pricing differences as well:

<td class="align-c numeric">
  3
</td>

<td class="align-c numeric">
  3
</td>

<td class="align-c numeric">
  6
</td>

<td class="align-c numeric">
  6
</td>

|                       | LOCALLY REDUNDANT STORAGE (LRS)                                           | ZONE REDUNDANT STORAGE (ZRS)                                                                            | GEOGRAPHICALLY REDUNDANT STORAGE (GRS)                                                       | READ-ACCESS GEOGRAPHICALLY REDUNDANT STORAGE (RA-GRS)                                       |
| --------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| How it works          | Makes multiple synchronous copies of your data within a single datacenter | Stores three copies of data across multiple datacenters within or across regions. For block blobs only. | Same as LRS, plus multiple asynchronous copies to a second datacenter hundreds of miles away | Same as GRS, plus read access to the secondary datacenter                                   |
| Total copies          |
| Why use it            | For economical local storage or data governance compliance                | An economical, higher durability option for block blob storage                                          | For protection against a major datacenter outage or disaster                                 | Provides read access to data during an outage, for maximum data availability and durability |
| Availability SLA      | 99.9% read/write                                                          | 99.9% read/write                                                                                        | 99.9% read/write                                                                             | 99.9% write  
99.99% read                                                                   |
| Pricing for first 1TB | <span class="price-data" data-amount="0.024">$0.024</span> per GB         | <span class="price-data" data-amount="0.03">$0.03</span> per GB                                         | <span class="price-data" data-amount="0.048">$0.048</span> per GB                            | <span class="price-data" data-amount="0.061">$0.061</span> per GB                           |

<pre>Taken from: http://azure.microsoft.com/en-us/pricing/details/storage/

</pre>

When designing an Azure infrastructure, it&#8217;s important to look into the different storage options . The disks should be distributed in storage accounts with geo-redundant and locally redundant settings based on the purpose of the disk:

[<img title="image" src="http://blogs.technet.com/cfs-file.ashx/__key/communityserver-blogs-components-weblogfiles/00-00-00-85-24-metablogapi/image_5F00_thumb_5F00_2A926D84.png" alt="image" width="660" height="228" border="0" />](http://blogs.technet.com/cfs-file.ashx/__key/communityserver-blogs-components-weblogfiles/00-00-00-85-24-metablogapi/image_5F00_5AB9B847.png)

It is important to set the storage account for the data disk(s) containing the SQL data and logs to locally redundant in order maintain accurate time stamps in the event of a DR situation requiring a full recovery.

## Geo-Replication concerns for SQL Disks

Geo-replication in Azure disks does not support the data file and log file of the same database to be stored on separate disks. GRS replicates changes on each disk independently and asynchronously. This mechanism does not guarantee the write order across geo-replicated copies of multiple disks. If you configure a database to store its data file and its log file on separate disks, the recovered disks after a disaster may contain a more up-to-date copy of the data file than the log file. If you do not have the option to disable geo-replication on the storage account, **you should keep all data and log files for a given database on the same disk.** If you must use more than one disk due to the size of the database, you need to deploy one of the disaster recovery solutions listed above to ensure data redundancy.

>  <a href="http://msdn.microsoft.com/en-us/library/azure/jj870962#BKMK_GEO" target="_blank">http://msdn.microsoft.com/en-us/library/azure/jj870962#BKMK_GEO</a>

## Conclusion

I hope this blogpost made it clear that you have a lot of different Azure redundancy options and when designing your disaster continuity for your different workloads it&#8217;s important to keep in mind that some workloads (like SQL) might have some concerns with Geo-Replication.

&nbsp;

Thanks,

Alexandre Verkinderen