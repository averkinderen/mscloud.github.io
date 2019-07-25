---
id: 9581
title: Azure Subscriptions best practices
date: 2016-01-22T10:31:50+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=9581
permalink: /azure-subscriptions-best-practices/
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
  - "20914"
  - "20914"
  - "20914"
categories:
  - Azure
tags:
  - azure
  - subscriptions
---
To be able to use all the stuff that Azure offers you will need a Subscription. If you are on your own or are just testing the different Azure capabilities in your lab you can easily create a trial Azure subscription and start using it.  [https://azure.microsoft.com/en-us/pricing/free-trial/](https://azure.microsoft.com/en-us/pricing/free-trial/ "https://azure.microsoft.com/en-us/pricing/free-trial/")

But if you need to deploy Azure in an enterprise with different teams, locations, etc it might get more complicated and you will need different subscriptions. This blog post will cover some of the Azure subscription best practices to keep in mind.

## What is a subscription?

At first a subscription was the administrative security boundary of Azure. Let’s say you had a HR team and a marketing team and no administrative overlap is allowed you would have to create two subscriptions. Now with the Azure Resource Management (ARM) model this is not longer the case as the subscription is no longer needed as an administrative boundary.

ARM provides a more granular Role-Based Access Control (RBAC) model for assigning administrative privileges at the resource level. RBAC is generally available now with 29 new roles available at this time. For a full list of RBAC roles have a look here <a href="https://azure.microsoft.com/en-us/documentation/articles/role-based-access-built-in-roles/" target="_blank">https://azure.microsoft.com/en-us/documentation/articles/role-based-access-built-in-roles/</a> .

A subscription forms the billing unit. What you have consumed from Azure within a subscription will be counted towards the Subscription bill.

A subscription also has a logical limit of scale of resources that can be allocated. There is a default limit for example of 6 SQL database servers and max 150 per subscription.  Many of these soft limits can be increased greatly by simply creating a support request, but some of the hard limits have a big impact on decisions regarding subscription design. Not all limit usages are visible in the Azure portal but you can use **Get-SubscriptionLimit ** PowerShell script that you can find here [Services Automation Repository](http://aka.ms/AutomationRepository).

You can find the full list of limits here [https://azure.microsoft.com/en-us/documentation/articles/azure-subscription-service-limits/](https://azure.microsoft.com/en-us/documentation/articles/azure-subscription-service-limits/ "https://azure.microsoft.com/en-us/documentation/articles/azure-subscription-service-limits/") . Scalability and capacity planning are a key element when designing a subscription strategy.

## Design considerations

It is critical when starting to design your Azure subscriptions to have a thorough understanding of the current and further environment and needs. You will have to design your subscription together with your Azure storage, network, administration and availability models and teams as each component can have an impact on the other with respect to scalability and flexibility. A bad subscription design can have a big impact on the long term. As the enterprise can find itself:

  * inceasing management of IP address space allocation
  * increasing costs of routing and firewall configurations
  * duplucating services required for example monitoring, anti-virus, patching, backup, etc
  * purchasing more dedicated network than bandwith is needed

Following is an example subscription design based on a subscription per Organizational Unit.

[<img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/01/image_thumb1.png" alt="image" width="244" height="123" border="0" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/01/image1.png)

Here is another example subscription design that is based on one subscription per environment in the development process of an application.

[<img style="background-image: none; padding-top: 0px; padding-left: 0px; margin: 0px; display: inline; padding-right: 0px; border-width: 0px;" title="image" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/01/image_thumb2.png" alt="image" width="244" height="125" border="0" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/01/image2.png)

For CSP-managed scenarios, here is an example subscription design that illustrates a model for one or more subscription per specific customer where a separate service deployment for a given customer may be assigned a dedicated subscription.

<a href="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/01/csp.png" rel="attachment wp-att-9811"><img class="alignnone size-medium wp-image-9811" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/01/csp-300x158.png" alt="CSP" width="300" height="158" srcset="/wp-content/uploads/2016/01/csp-300x158.png 300w, /wp-content/uploads/2016/01/csp-768x403.png 768w, /wp-content/uploads/2016/01/csp-1024x538.png 1024w, /wp-content/uploads/2016/01/csp.png 1500w" sizes="(max-width: 300px) 100vw, 300px" /></a>

Following is an architecture example for enterprise:

<a href="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/01/enterprise.png" rel="attachment wp-att-9831"><img class="alignnone size-medium wp-image-9831" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/01/enterprise-300x162.png" alt="enterprise" width="300" height="162" srcset="/wp-content/uploads/2016/01/enterprise-300x162.png 300w, /wp-content/uploads/2016/01/enterprise-768x416.png 768w, /wp-content/uploads/2016/01/enterprise-1024x554.png 1024w, /wp-content/uploads/2016/01/enterprise.png 1526w" sizes="(max-width: 300px) 100vw, 300px" /></a>

In this example we have multiple subscriptions, a tier 0 subscription for everything related to identity and authentication, a tier 1 for the Q&A environment and another tier 1 for the production environment. This will ensure that no change on the Q&A and production environment will have an impact on the identity and authentication environment and although the identity is in a separate subscription it will still be able to offer domain authentication services to the other subscriptions and virtual machines.

This model will scale based on needs. If you ever need to add another Q&A ennvironment or another production environment in another Azure region it&#8217;s perfectly possible.

### Connectivity

Connectivity and networking is really a key component when defining you subscription strategy. A virtual network needs to reside inside a subscription. A network can be a shared resouce inside an organization but that&#8217;s not always the case for a subscription. Because a virtual network exists inside a subscription you also need to consider the limitations. You can for example only have 50 virtual networks per subscription, 10 express routes per subscriptions and 10 virtual networks per express routes. So if you are using 2 express routes you can only have 20 virtual networks in one subscription. Keep in mind that if multiple virtual networks are using the same expressroute there is no network isolation. If network isolation is important to you, you should use Network Security groups to separate the traffic.

You can also use the express route accross different subscriptions as discussed here: <a href="https://azure.microsoft.com/en-us/blog/enable-multiple-subscription-expressroute/" target="_blank">https://azure.microsoft.com/en-us/blog/enable-multiple-subscription-expressroute/</a>

### Administration

A subscription is a logical boundary and grouping of Azure services and administration. Subscription administrators can provision, start and stop and delete Azure services. They can remove, add, read, write and download anything from the Azure storage account. They can grant administrative access to new users as well. So a subscription administrator is a really powerfull role and you need to think carefully for the people you assign this role. You can compare it to an Active Directory domain administrator.

When designing your subscriptions you should ask yourself the following questions:

  * Is the subscription owned by the customer or managed by a cloud service provider?
  * Is an Office 365 Azure Active Directory tenant set up?
  * Are there plans for Office 365 enrollment?
  * Are there other Azure subscriptions in use?
  * Have you deployed a trial Azure subscription?
  * Have you run a trial Power BI evaluation?
  * Have you run a RMS evaluation?
  * Can you use the desired OrgID *.onmicrosoft.com for company directory?

### Scale

As ex<a href="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/01/Azure-websites4.png" rel="attachment wp-att-9761"><img class="wp-image-9761 alignleft" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/01/Azure-websites4.png" alt="Azure-websites4" width="171" height="108" /></a>plained above a subscription has his limits in respect to the number of VMs you can run, virtual networks you can have, storage, etc.

&nbsp;

&nbsp;

So when defining your subscription design ask yourself the following questions:

  * What are the growth plans?
  * How will limited resources be allocated?
  * How will the model evolve over time considering additional users, shared access, and resource limits?

&nbsp;

## Subscription Naming Convention

When defining a naming convention for the subscriptions try to be as clear and meaningfull as possible. many organizations will have more than one subscription so you need to define a naming convention and be consistent.

You could use for example the followin naming convention:

  * **Contoso HR Business Dev**
  * **Contoso HR Business Prod**
  * **Contoso Sales Consumer Prod**

Which translates into: &#8220;Company&#8221; &#8220;Department&#8221; &#8220;Product line&#8221; &#8220;Environment&#8221;. This of course is just an example, the most important point here to remember is to define a naming convention that is meaningfull to the company.

&nbsp;

Hope this helps,

Alexandre Verkinderen

&nbsp;

PS: credits to the Azure documentation team and the Hybrid Cloud Azure Reference Architecture
