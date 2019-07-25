---
id: 9301
title: What is Microsoft Azure Stack?
date: 2015-11-07T16:11:33+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=9301
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
  - "5376"
  - "5376"
  - "5376"
image: /wp-content/uploads/2015/11/Alb8bAud50.png
categories:
  - Azure
  - MAS
  - WAP
tags:
  - azure
  - MAS
---
A lot is happening those days on the Microsoft public and private cloud front. Microsoft announced Azure stack at Ignite in Chigaco but I still see a lot of confusion on what Azure Stack exactly is.

### Azure Stack is a new cloud platform solution

Microsoft Azure Stack is new cloud platform solution that enables Azure capabilities in your datacenter. Just to be clear it is **NOT** an update on Windows Azure Pack that is available today. Available today, the Windows Azure Pack represents the cloud service **delivery experience replicated** for on-premises environments &#8211; this includes a portal and a select set of Azure-consistent services (such as web sites, service bus, etc). So it delivered the same Azure like experience but in the back-end it was totally different than Azure. Azure Pack will continue to be supported for Windows Server/ System Center 2016 and Windows Server/ System Center 2012 R2 deployments through at least 2017, with security updates through 2022.

Microsoft Azure Stack or MAS is totally new product that enables IT Pros and developers to build and deploy cloud applications and deploy it anywhere across any datacenter. The key to be able to do this is **consistency** between MAS and Azure. It includes Azure-inspired infrastructure and a next-generation service delivery experience and APIs with an expanded set of IaaS | PaaS services that are exactly the same as in Azure. It also includes Azure Resource Manager &#8211; the API and service management layer &#8211; thereby enabling “write once, deploy anywhere”.

&nbsp;

[<img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/11/image_thumb2.png" alt="image" width="644" height="307" border="0" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/11/image2.png)

&nbsp;

### Is there a migration path to Azure Stack?

Azure Stack is totally new product, it’s not a new version or an update on Windows Azure pack. So an in place upgrade will certainly not be possible. Microsoft is still looking on the technical approach on how to relocate any existing workloads from WAP to MAS.

### What makes up the Azure Stack?

Azure Stack is comprised of the following capabilities that are deployed on-premise:

Consistent Azure-based services:

  * Azure portal, based on the next-gen UX framework that is being rolled out in Azure as we speak
  * Azure Resource Manager – a declarative, template-based service management and API technology that helps specify and configure applications for automated deployment
  * PaaS services &#8211; Azure Service Fabric
  * IaaS services – Virtual Machines, Storage Accounts (Blobs | Tables), and Virtual Networks

[<img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/11/image_thumb3.png" alt="image" width="644" height="276" border="0" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/11/image3.png)

Cloud-inspired infrastructure, which includes:

  * Software-defined infrastructure platform – Storage | Compute | Networking | Security [powered by Windows Server, Hyper-V, and Azure based technologies]

  * Infrastructure management

[<img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/11/image_thumb4.png" alt="image" width="644" height="287" border="0" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/11/image4.png)

Not all Azure services will be brought to Azure Stack. The initial version of Azure Stack will have the following Azure-based services:

  * IaaS services – Virtual Machines, Storage Accounts (Blobs | Tables), and Virtual Networks
  * PaaS services – Azure Service Fabric
  * Azure Resource Manager, including core service management capabilities and extensible APIs

### Azure Resource Manager

Microsoft Azure Stack empowers application innovation by enabling “write once, deploy anywhere” across on-premises, service provider, and Microsoft Azure environments.

[<img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/11/image_thumb5.png" alt="image" width="644" height="342" border="0" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/11/image5.png)

Capabilities like Azure Resource Manager enable application owners to declare and target an application to Azure or Azure Stack. Azure Stack brings a rich set of Azure IaaS and PaaS services to on-premises environments, along with the exact same development tools and self-service experience and APIs.

[<img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/11/image_thumb6.png" alt="image" width="644" height="327" border="0" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/11/image6.png)

### Role based access

One of the top request for WAP is Role-based access control. As MAS is using the same ARM, API’s etc like in Azure we can also use the same RBAC model like in Azure. This means you can allow secure access with granular permissions to resources and assign resources to users, groups or service principals. Built-in roles like Readers, Contributors, Owners will make it easy to get started. First you will have to define Role definitions that desribes a set of permissions like read, write, delete actions etc. Next you associate a role definition with an identiy (user, group, etc) at a certain scope (resource group, resources, etc) which is called Role assignment.

[<img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/11/image_thumb7.png" alt="image" width="644" height="389" border="0" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/11/image7.png)

&nbsp;

### Conclusion

All of this is very exciting but as we are in an early phase now we still have to wait a litle longer. No time-frames have been announced yet but if you need more information please have a look here: http://blogs.technet.com/b/charlesjoy/archive/2015/05/06/azurestack-msignite.aspx

&nbsp;

Thanks,

Alexandre Verkinderen
