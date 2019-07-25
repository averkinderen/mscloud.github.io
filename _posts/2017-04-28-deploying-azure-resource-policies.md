---
id: 19131
title: Deploying Azure Resource Policies
date: 2017-04-28T09:03:13+10:00
author: alexandre@verkinderen.com
guid: http://www.mscloud.be/?p=19131
sc_member_order:
  - "0"
  - "0"
  - "0"
bpxl_standard_excerpt_home:
  - "0"
  - "0"
bpxl_standard_single_hide:
  - "0"
  - "0"
bpxl_image_excerpt_home:
  - "0"
  - "0"
bpxl_image_single_hide:
  - "0"
  - "0"
bpxl_audio_excerpt_home:
  - "0"
  - "0"
bpxl_audio_single_hide:
  - "0"
  - "0"
bpxl_video_excerpt_home:
  - "0"
  - "0"
bpxl_video_single_hide:
  - "0"
  - "0"
bpxl_link_excerpt_home:
  - "0"
  - "0"
bpxl_link_single_hide:
  - "0"
  - "0"
bpxl_gallery_excerpt_home:
  - "0"
  - "0"
bpxl_gallery_single_hide:
  - "0"
  - "0"
bpxl_status_excerpt_home:
  - "0"
  - "0"
bpxl_status_single_hide:
  - "0"
  - "0"
bpxl_singlerelated:
  - "0"
  - "0"
post_views_count:
  - "5941"
  - "5941"
image: /wp-content/uploads/2017/04/resource-group-tagging-150x150.png
categories:
  - Azure
  - Powershell
tags:
  - Azure
  - Governance
  - Policy
  - powershell
  - Tags
---
Hi all,

Before deploying anything in Azure you should think about Governance. You must address the topic of governance early to ensure the successful use of the cloud within your enterprise.  After a series of really intense governance workshops my customer was ready to apply the decisions made from those workshops in Azure. In those workshops we define for example:

### Naming conventions

Well-designed naming standards enable you to identify resources in the Azure portal, on an invoice, and within PowerShell scripts. Most likely, you already have naming standards for your on-premise infrastructure. When adding Azure to your environment, you should extend, and be consistent with those naming standards to your Azure resources. Naming standard facilitate more efficient management of the environment at all levels. Review and adopt where possible the <a href="https://docs.microsoft.com/en-us/azure/guidance/guidance-naming-conventions" data-linktype="relative-path">Patterns and Practices guidance</a>.

### Resource tags

<p class="lf-text-block lf-block" data-lf-anchor-id="05b5ce6bcfba22f913cd916fdf214b31:0">
  As users in your organization add resources to the Azure subscription, it becomes increasingly important to associate resources with the appropriate department, owner, and environment. You can attach metadata to resources through <a href="https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags" data-linktype="relative-path">tags</a>. You use tags to provide information about the resource or the owner. Tags enable you to not only aggregate and group resources in various ways, but also to use that data for the purposes of chargeback. You can tag resources with up to 15 key:value pairs.
</p>

<p class="lf-text-block lf-block" data-lf-anchor-id="97fbc41356ecf93a3acd08579a795e31:0">
  Resource tags are flexible and should be attached to most resources. Examples of common resource tags are:
</p>

<ul class="lf-text-block lf-block" data-lf-anchor-id="3d1e55cf59d96636d5c865591a2a32d3:0">
  <li>
    BillTo
  </li>
  <li>
    Department (or Business Unit)
  </li>
  <li>
    Environment (Production, Stage, Development)
  </li>
  <li>
    Tier (Web Tier, Application Tier)
  </li>
  <li>
    Application Owner
  </li>
  <li>
    ProjectName
  </li>
</ul>

[<img class="alignnone size-full wp-image-19231" src="http://www.mscloud.be/wp-content/uploads/2017/04/resource-group-tagging.png" alt="" width="400" height="243" srcset="/wp-content/uploads/2017/04/resource-group-tagging.png 400w, /wp-content/uploads/2017/04/resource-group-tagging-300x182.png 300w" sizes="(max-width: 400px) 100vw, 400px" />](http://www.mscloud.be/wp-content/uploads/2017/04/resource-group-tagging.png)

### Locations

To address data sovereignty issues, my customer only wanted to allow Azure Resources to be deployed in 2 specific regions whereas Azure provides regions across the world. Enterprises often wish to control where resources are created (whether to ensure data sovereignty or just to ensure resources are created close to the end consumers of the resources).

One way of applying these governance decisions is with [Azure Resource Policies](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-policy).

> Resource policies enable you to establish conventions for resources in your organization. By defining conventions, you can control costs and more easily manage your resources. For example, you can specify that only certain types of virtual machines are allowed, or you can require that all resources have a particular tag. Policies are inherited by all child resources. So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.

<p class="lf-text-block lf-block" data-lf-anchor-id="4010e30649f829048945178796204061:0">
  In this blog post and the upcoming two blogposts I will show you how you can create JSON Azure Resource Policy templates and re-use those policies in multiple different environments. There are two concepts to understand about policies:
</p>

<ul class="lf-text-block lf-block" data-lf-anchor-id="a48d0b17cbd3e0a00cc918526521db55:0">
  <li>
    Policy definition &#8211; you describe when the policy is enforced and what action to take (we will define this in a JSON file)
  </li>
  <li>
    Policy assignment &#8211; you apply the policy definition to a scope (subscription or resource group). This will be a Deployment PowerShell Script.
  </li>
</ul>

As I need to create and assign more than one resource policy I&#8217;m going to script the Policy deployment and assignment. The script will have the policy JSON file as an input and deploy it to the Azure subscription.

  1. This blogpost will cover how to create a deployment Powershell Script to deploy and assign Resource policies. We will then deploy a tagging policy as an example
  2. In the second blogpost we will deploy a Location policy to limit the Azure locations and ensure data souvereignty
  3. In the last blogpost we will deploy a policy to enforce our naming convention

## Policy Definition

<p class="lf-text-block lf-block" data-lf-anchor-id="44e7ab1b45d324a026c1115867705be5:0">
  Let&#8217;s create our resource policies definition based on JSON. The policy definition contains elements for:
</p>

<ul class="lf-text-block lf-block" data-lf-anchor-id="f07e837483564d4c497933d9266e22b4:0">
  <li>
    parameters
  </li>
  <li>
    display name
  </li>
  <li>
    description
  </li>
  <li>
    policy rule <ul>
      <li>
        logical evaluation
      </li>
      <li>
        effect
      </li>
    </ul>
  </li>
</ul>

Have a look [here](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-policy#policy-definition-structure) for more information regarding policy constructs. You first start with a policy definition that’s created using JSON (you can see the schema here: http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json) and which consists of one or more logical or condition operators that define the action and effect of the policy when a specific condition is achieved. So in our scenario we are checking **if** the field **tags**  is **false** then **append** the field tag with a **tag name** and a **default value**. You can find the Resource policy I created below:

<script src="https://gist.github.com/averkinderen/653d1226b17102d1e099845149402e6b.js"></script>
In this example we were applying Append, but there are more:

  * **Deny**: Blocks the resource request
  * **Audit**: Allows the request but adds a line to the activity log (which can be used to provide alerts or to trigger runbooks)
  * **Append**: Adds specified information to the resource. For example, if there is not a &#8220;CostCenter&#8221; tag on a resource, add that tag with a default value.

Any new resources created within the specified subscription will have those tags that we defined in our JSON file appended to it.

## Assigning Azure Resource Policies with PowerShell

Now that we have our tags defined we need to deploy and assign the policy to our Azure subscription. As I will deploy more than one policy I&#8217;m going to use PowerShell to make my life easier. Before proceeding with the PowerShell script, make sure you have <a href="https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps" data-linktype="absolute-path">installed the latest version</a> of Azure PowerShell. Policy parameters were added in version 3.6.0. If you have an earlier version, the script returns an error indicating the parameter cannot be found.

The script requires the following parameters:

  * Policy name
  * Policy description
  * Policy file (this is the full path to the JSON policy definition file)

You then need to specify the subscription to assign the Policy definition. Policies are inherited by all child resources. So, if a policy is applied to a subscription, it is applicable to all the resource groups and resources in that subscription.

    View the code on <script src="https://gist.github.com/averkinderen/df7bb438bd9908af73c0deb25879d654.js"></script>


Run the above script with the required parameters:

[<img class="alignnone size-large wp-image-19341" src="http://www.mscloud.be/wp-content/uploads/2017/04/ps2-1024x504.png" alt="" width="768" height="378" srcset="/wp-content/uploads/2017/04/ps2-1024x504.png 1024w, /wp-content/uploads/2017/04/ps2-300x148.png 300w, /wp-content/uploads/2017/04/ps2-768x378.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](http://www.mscloud.be/wp-content/uploads/2017/04/ps2.png)

That&#8217;s it! You have now created a new Azure Resource Policy definition and assigned that Policy to a subscription!

## Conclusion

After running the script and assigning the tagging policy you should see the following policy assigned to our subscription:

[<img class="alignnone size-large wp-image-19271" src="http://www.mscloud.be/wp-content/uploads/2017/04/sub-1024x419.png" alt="" width="768" height="314" srcset="/wp-content/uploads/2017/04/sub-1024x419.png 1024w, /wp-content/uploads/2017/04/sub-300x123.png 300w, /wp-content/uploads/2017/04/sub-768x314.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](http://www.mscloud.be/wp-content/uploads/2017/04/sub.png)

and as you can see, when we create a new resource without tags, they willl be appended automatically:

[<img class="alignnone size-large wp-image-19301" src="http://www.mscloud.be/wp-content/uploads/2017/04/tags-1024x604.png" alt="" width="768" height="453" srcset="/wp-content/uploads/2017/04/tags-1024x604.png 1024w, /wp-content/uploads/2017/04/tags-300x177.png 300w, /wp-content/uploads/2017/04/tags-768x453.png 768w, /wp-content/uploads/2017/04/tags.png 1445w" sizes="(max-width: 768px) 100vw, 768px" />](http://www.mscloud.be/wp-content/uploads/2017/04/tags.png)

In the next blog post we will use the same PowerShell script but create and assign a policy to limit the Azure regions. So stay tuned!

Hope this helps,

Alexandre
