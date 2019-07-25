---
id: 10721
title: Configuring Azure SQL DB Active-Geo replication
date: 2016-07-14T02:28:08+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=10721
permalink: /configuring-azure-sql-db-active-geo-replication/
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
  - "3293"
  - "3293"
  - "3293"
categories:
  - Azure
tags:
  - azure
  - sql
---
One of my customers is looking into migrating his SQL environment to Azure SQL DB. When migrating to a new platform, business continuity is key. When looking at the different availability solutions for Azure SQL DB we decided that for some business critical databases the Azure SQL DB standard tier with geo-replication and 1 standby secondary database was just not enough.

The premium tier of Azure SQL DB offers you **ACTIVE** geo replication with up-to 4 readable secondary databases! You can find an overview of the different Azure SQL Database Single-database service tiers here:

[<img class="alignleft size-medium wp-image-10751" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/07/service-tiers-300x158.png" alt="service tiers" width="300" height="158" srcset="/wp-content/uploads/2016/07/service-tiers-300x158.png 300w, /wp-content/uploads/2016/07/service-tiers-768x404.png 768w, /wp-content/uploads/2016/07/service-tiers-1024x538.png 1024w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/07/service-tiers.png)

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

In this blogpost I will describe the different business continuity solutions Azure SQL Database offers and how you can configure Active geo-replication to protect your databases. But let’s have a look first at the differences between standard and active geo-replication.

# Standard GEO-replication

Built on the same continuous copy mechanism as Active Geo-Replication, Standard Geo-Replication asynchronously replicates committed transactions from the primary database to one secondary database. The secondary, unlike Active Geo-Replication, is offline and does not accept client connections.

The offline secondary can be switched to active if there is a datacenter issue resulting in unavailability of the primary database. In such an event, the failover property of the database is enabled. This will activate the offline databases and making it an independent database ready to accept client connections.

The target region for the offline secondary is predetermined based on the location of your primary database.

[<img class="alignleft size-medium wp-image-10761" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/07/standard-300x156.png" alt="standard" width="300" height="156" srcset="/wp-content/uploads/2016/07/standard-300x156.png 300w, /wp-content/uploads/2016/07/standard-768x398.png 768w, /wp-content/uploads/2016/07/standard-1024x531.png 1024w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/07/standard.png)

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

When planning to use Standard Geo-Replication, consider the following:

  * The secondary database has the same service tier and performance level as the primary database. Ensure you have enough capacity on the server for your offline secondary. In addition, the collation setting is replicated from the primary to the offline secondary.
  * The offline secondary counts towards the maximum number of databases on a server.
  * The offline secondary counts toward the maximum allowed replicas in Active Geo-Replication. This means if you decide to use an offline secondary, you will be limited to three active secondary replicas. The source and target servers must belong to the same subscription.

# Active GEO-replication

The Active Geo-Replication feature implements a mechanism to provide database redundancy within the same Microsoft Azure region or in different regions (geo-redundancy). Active Geo-Replication asynchronously replicates committed transactions from a database to up to four copies of the database on different servers, using read committed snapshot isolation (RCSI) for isolation. When Active Geo-Replication is configured a secondary database is created on the specified server. The original database becomes the primary database. The primary database asynchronously replicates committed transactions to each of the secondary databases.

[<img class="alignleft size-medium wp-image-10771" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/07/active-300x152.png" alt="active" width="300" height="152" srcset="/wp-content/uploads/2016/07/active-300x152.png 300w, /wp-content/uploads/2016/07/active-768x390.png 768w, /wp-content/uploads/2016/07/active-1024x520.png 1024w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/07/active.png)

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

One of the primary benefits of Active Geo-Replication is that it provides a database-level disaster recovery solution with very low recovery time. When you place the secondary database on a server in a different region you add maximum resilience to your application. The cross-region redundancy enables applications to recover from a permanent loss of an entire datacenter or parts of a datacenter caused by natural disasters, catastrophic human errors, or malicious acts.

Another key benefit is that the secondary databases are readable and can be used to offload read-only workloads such as reporting jobs.

# Configuring Active GEO-Replication

How do you need to configure Active GEO-replication? If you have a running Azure **Premium** SQL DB  you can very easily add a secondary database.

The following steps create a new secondary database in a Geo-Replication partnership. The secondary database will have the same name as the primary database and will, by default, have the same service level. You can however change the service level of the secondary databases if required. The secondary database is readable and can be a single database or an elastic database. For more information, see [Service Tiers](https://azure.microsoft.com/en-us/documentation/articles/sql-database-service-tiers/). After the secondary is created and seeded, data will begin replicating from the primary database to the new secondary database.

  * In the [Azure portal](http://portal.azure.com/) browse to the database that you want to setup for Geo-Replication.
  * On the SQL Database blade, select **All settings** > **Geo-Replication**.
  * Select the region to create the secondary database.

[<img class="alignleft size-medium wp-image-10781" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/07/sec1-300x263.png" alt="sec1" width="300" height="263" srcset="/wp-content/uploads/2016/07/sec1-300x263.png 300w, /wp-content/uploads/2016/07/sec1-768x673.png 768w, /wp-content/uploads/2016/07/sec1.png 789w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/07/sec1.png)

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

  * Configure the **Secondary type** (**Readable**, or **Non-readable**).
  * Select or configure the server for the secondary database.

[<img class="alignleft size-full wp-image-10791" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/07/sec2.png" alt="sec2" width="244" height="130" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/07/sec2.png)

&nbsp;

&nbsp;

&nbsp;

&nbsp;

  * Click **Create** to add the secondary.
  * The secondary database is created and the seeding process begins.

[<img class="alignleft size-medium wp-image-10801" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/07/sec4-300x244.png" alt="sec4" width="300" height="244" srcset="/wp-content/uploads/2016/07/sec4-300x244.png 300w, /wp-content/uploads/2016/07/sec4-768x626.png 768w, /wp-content/uploads/2016/07/sec4-1024x835.png 1024w, /wp-content/uploads/2016/07/sec4.png 1308w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/07/sec4.png)

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

That’s it! In a few mouse clicks you have created a secondary failover database. You can use the same procedure to add another 3 databases, in different regions to increase your availability.

In the next blog post we are going to cover the different failover mechanisme of our newly protected Azure SQL Database.

Thanks,

Alex
