---
id: 19734
title: How to define an Azure Limited Admin custom role
date: 2017-09-11T12:52:01+10:00
author: alexandre@verkinderen.com
layout: revision
guid: http://mscloud.be/19720-revision-v1/
permalink: /19720-revision-v1/
---
Hi all,

After implementing the Governance policies and foundations described in“<a href="http://mscloud.be/deploying-azure-resource-policies/" target="_blank" rel="noopener">Deploying Azure resource policies</a>” it is important to make sure the end-consumers will not be able to change or remove those policies. In the customer environment I’m currently working on we defined Azure Resource Policies to enforce tagging, naming conventions, allowed regions etc., but we also enforced some network and routing settings. We implemented a really secure routing and firewall environment with User Defined Routes, NSG’s, virtual appliances, auditing and tracking etc. So we need to make sure users are not able to delete or change those policies and governance settings. This can be done with Azure RBAC.

## Azure Role Based Access (RBAC)

Azure Role-based access control will allow the owners of a subscription to assign granular roles to other users who can manage specific resource scopes in their environment. RBAC allows the flexibility of owning one Azure subscription managed by the administrator account (service administrator role at a subscription level) and have multiple users invited to work under the same subscription but without any administrative rights for it. You can assign RBAC at 3 different levels:

  * Subscription level
  * Resource Group
  * Resource

For an overview of all the built-in user roles have a look here: [https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-built-in-roles](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-built-in-roles "https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-built-in-roles")

The challenge today in Azure Role based access is that it’s really difficult to allow a user to create and delete anything in Azure (as we want to encourage users to test and play and discover) but at the same time make sure our policies and networking settings cannot me modified. I call this the &#8220;Limited Admin&#8221; User Role.

The solution is to create a new Custom Role.

## Azure Custom Role

Create a custom role in Azure Role-Based Access Control (RBAC) if none of the built-in roles meet your specific access needs. Custom roles can be created using [Azure PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), [Azure Command-Line Interface](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli) (CLI), and the [REST API](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest). Just like built-in roles, you can assign custom roles to users, groups, and applications at subscription, resource group, and resource scopes. Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.

Each tenant can create up to 2000 custom roles but my recommendation is to limit this as much as you can to limit the custom roles sprawl.

A JSON template can be used as the source definition for the custom role. The following example creates a custom role that will ensure the user can create and delete everything he wants but not the pre-defined network settings, UDR’s, NSG’s etc.

Create a new file `C:\Temp\LimitedAdmin.json` . The Id should be set to `null` on initial role creation as a new ID is generated automatically. Change the subscriptionID to match yours.

<div class="oembed-gist">
  <noscript>
    View the code on <a href="https://gist.github.com/averkinderen/af43d9e4c5d434356c8a0d3d99c3cdbd">Gist</a>.
  </noscript>
</div>

<p class="lf-text-block lf-block" data-lf-anchor-id="0d84286d56b8241b590d2d46b500c157:0">
  To add the role to the subscriptions, run the following PowerShell command:
</p>

<pre class="lang:ps decode:true ">Login-AzureRMAccount
New-AzureRmRoleDefinition -InputFile "C:\Temp\LimitedAdmin.json"</pre>

<p data-lf-anchor-id="0d84286d56b8241b590d2d46b500c157:0">
  Now login to the Azure Portal and you should see your newly created custom role:
</p>

<p data-lf-anchor-id="0d84286d56b8241b590d2d46b500c157:0">
  <img class="alignnone size-medium wp-image-19724" src="/wp-content/uploads/2017/09/limitedadmin-300x129.png" alt="" width="300" height="129" srcset="/wp-content/uploads/2017/09/limitedadmin-300x129.png 300w, /wp-content/uploads/2017/09/limitedadmin-768x331.png 768w, /wp-content/uploads/2017/09/limitedadmin.png 809w" sizes="(max-width: 300px) 100vw, 300px" />
</p>

<p data-lf-anchor-id="0d84286d56b8241b590d2d46b500c157:0">
  and the custom permissions can be seen here:
</p>

<p data-lf-anchor-id="0d84286d56b8241b590d2d46b500c157:0">
  <img class="alignnone size-medium wp-image-19725" src="/wp-content/uploads/2017/09/permissions-300x194.png" alt="" width="300" height="194" srcset="/wp-content/uploads/2017/09/permissions-300x194.png 300w, /wp-content/uploads/2017/09/permissions-768x497.png 768w, /wp-content/uploads/2017/09/permissions-1024x662.png 1024w, /wp-content/uploads/2017/09/permissions.png 1437w" sizes="(max-width: 300px) 100vw, 300px" />
</p>

<p data-lf-anchor-id="0d84286d56b8241b590d2d46b500c157:0">
  We have now created a new Azure Limited Admin by creating a new custom role.
</p>

<p data-lf-anchor-id="0d84286d56b8241b590d2d46b500c157:0">
  Hope this helps,
</p>

<p data-lf-anchor-id="0d84286d56b8241b590d2d46b500c157:0">
  Alex
</p>