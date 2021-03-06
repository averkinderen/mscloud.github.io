---
id: 19977
title: Cross subscription deployment with Azure Blueprints
date: 2019-03-24T10:04:34+10:00
author: alexandre@verkinderen.com
layout: revision
guid: https://mscloud.be/19960-revision-v1/
permalink: /19960-revision-v1/
---
A common design pattern in Azure is the Hub and Spoke topology as described [here](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/shared-services). In this blog post I will describe how you can deploy a spoke environment in a different subscription and enable VNET-peering to the hub environment with Blueprints. We assume that the Hub environment is already fully configured and deployed.

We are going to use an ARM [template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-existing-vnet-to-vnet-peering) as an artifact in our Blueprint that will do the following:

  1. Deploy a new VNET in our Spoke subscription
  2. Deploy new Spoke subnet
  3. Configure VNET peering from spoke-to-hub in our Spoke subscription
  4. Configure VNET peering from hub-to-spoke in our Hub subscription

To be able to configure VNET peering with Blueprints in another subscription we need to use an [Azure Managed Identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview) which is still in preview.

#### Azure Managed Identity

Managed identities for Azure resources provides Azure services with a managed identity in Azure Active Directory. You can use this identity to authenticate to services that support Azure AD authentication, without needing credentials in your code. We will be using User-assigned managed entity. 

  1. In the search box, type _Managed Identities_, and under **Services**, click **Managed Identities**.<figure class="wp-block-image">

[<img src="/wp-content/uploads/2019/03/managedidentity.png" alt="" class="wp-image-19961" srcset="/wp-content/uploads/2019/03/managedidentity.png 943w, /wp-content/uploads/2019/03/managedidentity-300x112.png 300w, /wp-content/uploads/2019/03/managedidentity-768x287.png 768w" sizes="(max-width: 943px) 100vw, 943px" />](/wp-content/uploads/2019/03/managedidentity.png)</figure> 

  1. Click **Add** and enter values in the following fields under **Create user assigned managed** identity pane:
      * **Resource Name**: This is the name for your user-assigned managed identity, for example **MI BLueprint**.
      * **Subscription**: Choose the subscription to create the user-assigned managed identity under
      * **Resource Group**: Create a new resource group to contain your user-assigned managed identity or choose **Use existing** to create the user-assigned managed identity in an existing resource group.
      * **Location**: Choose a location to deploy the user-assigned managed identity, for example **Australia East**.
  2. Click **Create**.
  3. Once created give the newly created managed identity the appropriate permissions on your hub and spoke subscription.

#### Vnet Peering with Blueprint

Download the Blueprint example from  
[https://github.com/averkinderen/Azure/tree/master/Blueprint-VNET-peering.](https://github.com/averkinderen/Azure/tree/master/Blueprint-VNET-peering) 

And use the import function of Jim&#8217;s Britt [PowerShell](https://github.com/JimGBritt/AzureBlueprint) script to import the Blueprint in your environment. Once imported, assign the blueprint to the spoke subscription and select the newly created managed entity:<figure class="wp-block-image">

[<img src="/wp-content/uploads/2019/03/mi5-1024x385.png" alt="" class="wp-image-19966" srcset="/wp-content/uploads/2019/03/mi5-1024x385.png 1024w, /wp-content/uploads/2019/03/mi5-300x113.png 300w, /wp-content/uploads/2019/03/mi5-768x288.png 768w" sizes="(max-width: 1024px) 100vw, 1024px" />](/wp-content/uploads/2019/03/mi5.png)</figure> 

After the assignment you can follow the progress in the activity log. Notice the operations that are using the newly created managed identity:<figure class="wp-block-image">

[<img src="/wp-content/uploads/2019/03/mi6-1024x437.png" alt="" class="wp-image-19967" srcset="/wp-content/uploads/2019/03/mi6-1024x437.png 1024w, /wp-content/uploads/2019/03/mi6-300x128.png 300w, /wp-content/uploads/2019/03/mi6-768x328.png 768w" sizes="(max-width: 1024px) 100vw, 1024px" />](/wp-content/uploads/2019/03/mi6.png)</figure> 

In a few seconds the deployment will be completed<figure class="wp-block-image">

[<img src="/wp-content/uploads/2019/03/mi7-1024x320.png" alt="" class="wp-image-19970" srcset="/wp-content/uploads/2019/03/mi7-1024x320.png 1024w, /wp-content/uploads/2019/03/mi7-300x94.png 300w, /wp-content/uploads/2019/03/mi7-768x240.png 768w" sizes="(max-width: 1024px) 100vw, 1024px" />](/wp-content/uploads/2019/03/mi7.png)</figure> 

Now, let&#8217;s have a look at the status of the VNET peering:<figure class="wp-block-image">

[<img src="/wp-content/uploads/2019/03/vnet-1024x355.png" alt="" class="wp-image-19969" srcset="/wp-content/uploads/2019/03/vnet-1024x355.png 1024w, /wp-content/uploads/2019/03/vnet-300x104.png 300w, /wp-content/uploads/2019/03/vnet-768x266.png 768w, /wp-content/uploads/2019/03/vnet.png 1110w" sizes="(max-width: 1024px) 100vw, 1024px" />](/wp-content/uploads/2019/03/vnet.png)</figure> 

As you can see, by using Azure Managed entity and Blueprints it&#8217;s now easier than ever to deploy cloud environments in a repeatable manner using composable artifacts. Every time we have a new spoke subscription we can assign the Blueprint and the vnet and peering will be configured automatically.

Hope this helps,  
Alex