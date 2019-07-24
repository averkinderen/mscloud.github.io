---
id: 19958
title: Accessing the Azure Fabric with forced tunneling enabled
date: 2019-02-02T15:32:25+10:00
author: alexandre@verkinderen.com
layout: revision
guid: https://mscloud.be/19953-revision-v1/
permalink: /19953-revision-v1/
---
A common scenario in a lot of companies is that no outgoing internet traffic is allowed from devices without going through policy enforcement services like firewalls, proxy services and other systems. The issue here is that by default every virtual machine you deploy in Azure has an outgoing route directly to the internet. 

If we look at the default system routes we can see that the next hop for everything unknown is the internet.  


<table class="wp-block-table">
  <tr>
    <th>
      Source
    </th>
    
    <th>
      Address prefixes
    </th>
    
    <th>
      Next hop type
    </th>
  </tr>
  
  <tr>
    <td>
      Default
    </td>
    
    <td>
      Unique to the virtual network
    </td>
    
    <td>
      Virtual network
    </td>
  </tr>
  
  <tr>
    <td>
      Default
    </td>
    
    <td>
      0.0.0.0/0
    </td>
    
    <td>
      Internet
    </td>
  </tr>
</table>

### The 0.0.0.0/0 route

The 0.0.0.0/0 prefix contains everything that is not defined in another vnet or subnet. So if you go from an Azure VM to facebook.com for example it will hit this route and the next hop will be the internet. **The only exception is Azure Services.** Azure services like storage accounts, keyvault and others will also be catched by this 0.0.0.0/0 route but although the next hop is Internet this traffic will never leave the Azure backbone. So if the destination address is for one of the Azure&#8217;s services, Azure routes the traffic directly to the service over Azure&#8217;s backbone network, rather than routing the traffic to the Internet. Even if the Azure services are in another region you will remain on the backbone and never go the public internet. On all of my virtual networks I enable Network Watcher and when visualizing the traffic on the world map I could see traffic flowing from my VM deployed in Australia East to East US, West US, South East Asia and many other Azure regions. The time sync of my vm would come from East US2 for example, the updates from West US and the licensing activation again from another region. Below is a summary of the traffic generated from my VM&#8217;s deployed in Australia East<figure class="wp-block-image">

<img src="/wp-content/uploads/2019/02/traffic-1024x483.png" alt="" class="wp-image-19954" srcset="/wp-content/uploads/2019/02/traffic-1024x483.png 1024w, /wp-content/uploads/2019/02/traffic-300x142.png 300w, /wp-content/uploads/2019/02/traffic-768x363.png 768w, /wp-content/uploads/2019/02/traffic.png 1544w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

### Issue

The big issue here is that if we change the default system routes to force all internet traffic down on-premises (as per company policy) through the gateway (like in the table below) all traffic to the Azure Fabric to reach Azure services will be send down on-premises as well. This means no management, no updates, no licenses etc

<table class="wp-block-table">
  <tr>
    <th>
      Source
    </th>
    
    <th>
      Address prefixes
    </th>
    
    <th>
      Next hop type
    </th>
  </tr>
  
  <tr>
    <td>
      Default
    </td>
    
    <td>
      Unique to the virtual network
    </td>
    
    <td>
      Virtual network
    </td>
  </tr>
  
  <tr>
    <td>
      User
    </td>
    
    <td>
      0.0.0.0/0
    </td>
    
    <td>
      Virtual network gateway
    </td>
  </tr>
</table>

But there is again an exception to what I just described above. If you enable a [service endpoint](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-service-endpoints-overview) for an Azure service, traffic to the service is not routed to the next hop type in a route with the 0.0.0.0/0 address prefix, because address prefixes for the service are specified in the route that Azure creates when you enable the service endpoint, and the address prefixes for the service are longer than 0.0.0.0/0. So you can attach the Storage Endpoint or KeyVault endpoint to your subnet and all internet traffic will flow down on-premises except storage and KeyVault traffic, that remains on the backbone. 

Sadly enough there are no endpoints for all Azure services. So we end up in the same boat as before and our machines don&#8217;t get a license or will not be backed up.

## Solution

The only solution to meet the company&#8217;s security requirements and still have fully workings VM&#8217;s is to create custom routes and inject the [public IP addresses of the Azure regions](https://www.microsoft.com/en-au/download/details.aspx?id=41653) in the route table.