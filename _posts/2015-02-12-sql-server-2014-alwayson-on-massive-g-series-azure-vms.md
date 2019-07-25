---
id: 5561
title: SQL Server 2014 AlwaysOn on Massive G-series Azure VMs
date: 2015-02-12T09:26:25+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=5561
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
  - "5309"
  - "5309"
  - "5309"
image: /wp-content/uploads/2015/02/Azure-SQL-Database-150x150.png
categories:
  - Azure
tags:
  - Azure
  - IAAS
  - sql
  - VM
---
In this blog post I&#8217;m going to test the recent availability of the massive G-Series VMs and ability to automate High Availability for SQL 2014.  The fact that Azure provides high availability mechanisms, such as service healing for cloud services and failure recovery detection for the Virtual Machines, does not itself guarantee you can meet the desired SLA. These mechanisms protect the high availability of the VMs but not the high availability of SQL Server running inside the VMs. It is possible for the SQL Server instance to fail while the VM is online and healthy. Moreover, even the high availability mechanisms provided by Azure allow for downtime of the VMs due to events such as recovery from software or hardware failures and operating system upgrades.

We will deploy SQL 2014 Alwayson on the G series vms!

> G-series sizes provide the most memory, the highest processing power and the largest amount of local SSD of any Virtual Machine size currently available in the public cloud. This extraordinary performance will allow customers to deploy very large scale-up enterprise applications. G-series offers up to 32 vCPUs using the latest [Intel® Xeon® processor E5 v3 family](http://www.intel.com/content/www/us/en/processors/xeon/xeon-e5-solutions.html), 448GB of memory, and 6.59 TB of local Solid State Drive (SSD) space. This powerful VM size easily handles deployments of mission critical applications such as large relational database servers (SQL Server, MySQL  etc.,) and large NoSQL databases (MongoDB, Cloudera, Cassandra etc.).

[<img class=" size-full wp-image-8251 aligncenter" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/2015-01-26-21.48.45.png" alt="2015-01-26 21.48.45" width="843" height="403" srcset="/wp-content/uploads/2015/02/2015-01-26-21.48.45.png 843w, /wp-content/uploads/2015/02/2015-01-26-21.48.45-300x143.png 300w, /wp-content/uploads/2015/02/2015-01-26-21.48.45-768x367.png 768w" sizes="(max-width: 843px) 100vw, 843px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/2015-01-26-21.48.45.png)

In the table below you can find an overview of the G-series (pretty impressive stuff if you ask me 🙂 )

### Standard tier – G series* {.subHeading}

<table style="height: 566px;" width="1381">
  <tr>
    <th>
      Size – Management Portal\cmdlets & APIs
    </th>
    
    <th>
      CPU cores
    </th>
    
    <th>
      Memory
    </th>
    
    <th>
      Max. disk sizes –<br /> virtual machine
    </th>
    
    <th>
      Max. data disks<br /> (1023 GB each)
    </th>
    
    <th>
      Max. IOPS<br /> (500 per disk)
    </th>
  </tr>
  
  <tr>
    <td>
      STANDARD_G1\(same)
    </td>
    
    <td>
      2
    </td>
    
    <td>
      28 GB
    </td>
    
    <td>
      OS = 127 GBLocal SSD disk = 384 GB
    </td>
    
    <td>
      4
    </td>
    
    <td>
      4 x 500
    </td>
  </tr>
  
  <tr>
    <td>
      STANDARD_G2\(same)
    </td>
    
    <td>
      4
    </td>
    
    <td>
      56 GB
    </td>
    
    <td>
      OS = 127 GBLocal SSD disk = 768 GB
    </td>
    
    <td>
      8
    </td>
    
    <td>
      8 x 500
    </td>
  </tr>
  
  <tr>
    <td>
      STANDARD_G3\(same)
    </td>
    
    <td>
      8
    </td>
    
    <td>
      112 GB
    </td>
    
    <td>
      OS = 127 GBLocal SSD disk = 1,536 GB
    </td>
    
    <td>
      16
    </td>
    
    <td>
      16 x 500
    </td>
  </tr>
  
  <tr>
    <td>
      STANDARD_G4\(same)
    </td>
    
    <td>
      16
    </td>
    
    <td>
      224 GB
    </td>
    
    <td>
      OS = 127 GBLocal SSD disk = 3,072 GB
    </td>
    
    <td>
      32
    </td>
    
    <td>
      32 x 500
    </td>
  </tr>
  
  <tr>
    <td>
      STANDARD_G5\(same)
    </td>
    
    <td>
      32
    </td>
    
    <td>
      448 GB
    </td>
    
    <td>
      OS = 127 GBLocal SSD disk = 6,144 GB
    </td>
    
    <td>
      64
    </td>
    
    <td>
      64 x 500
    </td>
  </tr>
</table>

In the new Azure portal you can find the new auto HA setup capabilities using the AlwaysOn Portal Template added for SQL Server in Azure VMs. You can also install SQL alwayson manually yourself but it requires quite a lot of configuration and virtual machines. A step by step overview can be found <a href="https://msdn.microsoft.com/en-us/library/azure/dn249504.aspx" target="_blank">here</a>.

If you don&#8217;t want to do it all by yourself and want to get started very quickly you can create a High available SQL Alwayson infrastructure in just a few mouse clicks. The SQL server 2014 Always on template that is available from the Azure galery will install the following:

[<img class="alignnone wp-image-5801 size-full" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/IC665510.gif" alt="IC665510" width="613" height="296" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/IC665510.gif)

Let&#8217;s get started!

  * On the Azure Management Portal, at the bottom left of the web page, click **+NEW**
  * On the **Create a Virtual Machine** page, you will see the new SQL Server 2014 Always on template
  * Click Create

[<img class="alignnone size-large wp-image-5571" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql1-1024x728.png" alt="sql1" width="768" height="546" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql1.png)

&nbsp;

  * Make sure to select WestUS or East US as region as the G-series VMs are not available in all the regions.
  * Specify a Resource Group name

> Resource groups are enabled by the new management functionality, Azure Resource Manager. Azure Resource Manager allows you to group multiple resources as a logical group which serves as the lifecycle boundary for every resource contained within it. Typically a group will contain resources related to a specific application. For example, a group may contain a Website resource that hosts your public website, a SQL Database that stores relational data used by the site, and a Storage Account that stores non-relational assets.

[<img class="alignnone wp-image-5562 size-large" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql01-347x1024.png" alt="sql01" width="347" height="1024" srcset="/wp-content/uploads/2015/02/sql01-347x1024.png 347w, /wp-content/uploads/2015/02/sql01-102x300.png 102w, /wp-content/uploads/2015/02/sql01.png 440w" sizes="(max-width: 347px) 100vw, 347px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql01.png)

  * Click on SQL server settings
  * Select a G serie VM. I&#8217;m going to deploy the G5 Series VMs 😉

[<img class="alignnone wp-image-5581 size-large" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql2-1024x777.png" alt="sql2" width="768" height="583" srcset="/wp-content/uploads/2015/02/sql2-1024x777.png 1024w, /wp-content/uploads/2015/02/sql2-300x228.png 300w, /wp-content/uploads/2015/02/sql2-768x583.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql2.png)

  * Next specify the Availability Group Name and Group Listener Name

> Availability Groups, released in SQL Server 2012 and enhanced in SQL Server 2014, detect conditions impacting SQL Server availability (e.g. SQL service being down or losing connectivity).  When detecting these conditions, the Availability Group fails over a group of databases to a secondary replica. In the context of Azure Infrastructure Services, this significantly increases the availability of these databases during Microsoft Azure’s VM Service Healing (e.g. due to physical hardware failures), platform upgrades, or your own patching of the guest OS or SQL Server.
> 
> Client applications connect to the primary replica of an availability group using an [Availability Group Listener](http://msdn.microsoft.com/en-us/library/hh213417.aspx?WT.mc_id=Blog_SQL_Announce_DI). The Listener specifies a DNS name that remains the same, irrespective of the number of replicas or where these are located.
> 
> For example: Server=tcp:_ListenerName_,1433;Database=_DatabaseName_;
> 
> To support this in Azure Virtual Machines, the Listener must be assigned the IP address of an Azure Load Balancer. The Load Balancer routes connections to endpoint of the primary replica of the Availability Group. This is done automatically for you in the template.

[<img class="alignnone wp-image-5591 size-full" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql3.png" alt="sql3" width="993" height="793" srcset="/wp-content/uploads/2015/02/sql3.png 993w, /wp-content/uploads/2015/02/sql3-300x240.png 300w, /wp-content/uploads/2015/02/sql3-768x613.png 768w" sizes="(max-width: 993px) 100vw, 993px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql3.png)

  * Next Create Storage account
  * For an overview of the different storage options have a look here <http://www.mscloud.be/azure-storage-redundancy-options/ >

[<img class="alignnone wp-image-5601 size-large" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql4-1024x819.png" alt="sql4" width="768" height="614" srcset="/wp-content/uploads/2015/02/sql4-1024x819.png 1024w, /wp-content/uploads/2015/02/sql4-300x240.png 300w, /wp-content/uploads/2015/02/sql4-768x614.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql4.png)

Click OK and then Create to launch the creation of the VMs.

This might  take a while as beside a new network and 3 new Active directory domains, new storage account and 8 virtual machines will be created!

  * You can follow the Progress in the event tabs

[<img class="alignnone wp-image-5611 size-large" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql5-775x1024.png" alt="sql5" width="768" height="1015" srcset="/wp-content/uploads/2015/02/sql5-775x1024.png 775w, /wp-content/uploads/2015/02/sql5-227x300.png 227w, /wp-content/uploads/2015/02/sql5-768x1015.png 768w, /wp-content/uploads/2015/02/sql5.png 906w" sizes="(max-width: 768px) 100vw, 768px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql5.png)

&nbsp;

In the ResourceGroup overview you can see all that will be deployed:

  * 1 new dedicated network
  * 3 new domains
  * 1 new storage account
  * 2 Domain controllers
  * 1 File Witness Server
  * 2 SQL servers

Can you imagine  you have to deploy and configure all of this yourself&#8230;

If you look at the newly created resource group, you have a quick overview of all the different components and the status. At the moment we are still deploying or creating the vm&#8217;s, so that&#8217;s why they are in a warning state.

[<img class="alignnone wp-image-5641 size-large" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql8-920x1024.png" alt="sql8" width="768" height="855" srcset="/wp-content/uploads/2015/02/sql8-920x1024.png 920w, /wp-content/uploads/2015/02/sql8-270x300.png 270w, /wp-content/uploads/2015/02/sql8-768x854.png 768w, /wp-content/uploads/2015/02/sql8.png 1165w" sizes="(max-width: 768px) 100vw, 768px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql8.png)

&nbsp;

Automatically a bunch of user roles are created for you. So you could integrated those roles with you Azure Active Directory for example.

[<img class="alignnone wp-image-5671 size-large" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql11-701x1024.png" alt="sql11" width="701" height="1024" srcset="/wp-content/uploads/2015/02/sql11-701x1024.png 701w, /wp-content/uploads/2015/02/sql11-205x300.png 205w, /wp-content/uploads/2015/02/sql11-768x1121.png 768w, /wp-content/uploads/2015/02/sql11.png 887w" sizes="(max-width: 701px) 100vw, 701px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql11.png)

  * You can also define metrics for easy diagnostics

[<img class="alignnone wp-image-5681 size-large" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql12-1024x627.png" alt="sql12" width="768" height="470" srcset="/wp-content/uploads/2015/02/sql12-1024x627.png 1024w, /wp-content/uploads/2015/02/sql12-300x184.png 300w, /wp-content/uploads/2015/02/sql12-768x470.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql12.png)

&nbsp;

Click on OK and Save

&nbsp;

[<img class="alignnone wp-image-5691 size-large" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql13-1024x627.png" alt="sql13" width="768" height="470" srcset="/wp-content/uploads/2015/02/sql13-1024x627.png 1024w, /wp-content/uploads/2015/02/sql13-300x184.png 300w, /wp-content/uploads/2015/02/sql13-768x470.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql13.png)

&nbsp;

So, after a few more coffees everything is deployed and ready to go!

[<img class="alignnone wp-image-5701 size-large" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql14-995x1024.png" alt="sql14" width="768" height="790" srcset="/wp-content/uploads/2015/02/sql14-995x1024.png 995w, /wp-content/uploads/2015/02/sql14-291x300.png 291w, /wp-content/uploads/2015/02/sql14-768x791.png 768w, /wp-content/uploads/2015/02/sql14.png 1155w" sizes="(max-width: 768px) 100vw, 768px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql14.png)

&nbsp;

Let&#8217;s remote desktop to my High available SQL servers!

&nbsp;

SQL Always on pre-configured !  So easy 🙂

[<img class="alignnone wp-image-5711 size-full" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql15.png" alt="sql15" width="669" height="664" srcset="/wp-content/uploads/2015/02/sql15.png 669w, /wp-content/uploads/2015/02/sql15-150x150.png 150w, /wp-content/uploads/2015/02/sql15-300x298.png 300w, /wp-content/uploads/2015/02/sql15-55x55.png 55w" sizes="(max-width: 669px) 100vw, 669px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sql15.png)

  * You can also connect from your local desktop directly using your SQL management studio as shown below

[<img class="alignnone wp-image-5731 size-full" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sqlserverinvmconnectionmap.png" alt="sqlserverinvmconnectionmap" width="802" height="444" srcset="/wp-content/uploads/2015/02/sqlserverinvmconnectionmap.png 802w, /wp-content/uploads/2015/02/sqlserverinvmconnectionmap-300x166.png 300w, /wp-content/uploads/2015/02/sqlserverinvmconnectionmap-768x425.png 768w" sizes="(max-width: 802px) 100vw, 802px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/sqlserverinvmconnectionmap.png)

&nbsp;

&nbsp;

## Conclusion

I was pretty impressed by how easy it is to deploy a high available SQL 2014 environment in just a few mouse clicks.
