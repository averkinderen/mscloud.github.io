---
id: 19431
title: 'Deploying Azure Resource Policies 2: Limit Azure Regions'
date: 2017-05-23T14:00:23+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://www.mscloud.be/?p=19431
permalink: /deploying-azure-resource-policies-2-limit-azure-regions/
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
  - "3452"
  - "3452"
categories:
  - Azure
tags:
  - Azure
  - Governance
  - Policy
  - powershell
---
This blogpost is the second blogpost of [applying governance](http://www.mscloud.be/deploying-azure-resource-policies/) in Azure.

Many organizations that are moving to Azure would like to enforce data sovereignty and ensure that no resources can be deployed outside of the country. One of my customers needed to make sure that no Azure resources would be deployed outside of Australia. This can easily be achieved with Azure Resource Policies.

Just like in the [first blogpost](http://www.mscloud.be/deploying-azure-resource-policies/) we need to create our Policy and then assign it.

First of all, we need to know the exact names of the Azure regions we want to allow. This can be achieved by running the following PowerShell cmdlet:

&nbsp;

<pre class="lang:ps decode:true">login-azurermaccount
Get-AzureRmLocation | Select Location, DisplayName</pre>

&nbsp;

[<img class="alignnone size-large wp-image-19441" src="http://www.mscloud.be/wp-content/uploads/2017/05/locations-759x1024.png" alt="" width="759" height="1024" srcset="/wp-content/uploads/2017/05/locations-759x1024.png 759w, /wp-content/uploads/2017/05/locations-222x300.png 222w, /wp-content/uploads/2017/05/locations-768x1036.png 768w, /wp-content/uploads/2017/05/locations.png 1391w" sizes="(max-width: 759px) 100vw, 759px" />](http://www.mscloud.be/wp-content/uploads/2017/05/locations.png)

# Create Azure Resource Policy:

The next step is to create a JSON Resource Policy that will deny the deployment of Azure Resources if it’s not deployed in Australia:

&nbsp;

<div class="oembed-gist">
  <noscript>
    View the code on <a href="https://gist.github.com/averkinderen/19991babc3d15b599c3fa6001d80b234">Gist</a>.
  </noscript>
</div>

# Assign Azure Resource Policy:

We will reuse our [PowerShell deployment script](https://gist.github.com/averkinderen/df7bb438bd9908af73c0deb25879d654) from the first blogpost to assign the policy on the subscription level.

[<img class="alignnone size-large wp-image-19461" src="http://www.mscloud.be/wp-content/uploads/2017/05/Policydeployment-1024x569.png" alt="" width="768" height="427" srcset="/wp-content/uploads/2017/05/Policydeployment-1024x569.png 1024w, /wp-content/uploads/2017/05/Policydeployment-300x167.png 300w, /wp-content/uploads/2017/05/Policydeployment-768x427.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](http://www.mscloud.be/wp-content/uploads/2017/05/Policydeployment.png)

That’s it, mission accomplished!

# Conclusion

After running the script and assigning the location policy you should see the following policy assigned to our subscription:

[<img class="alignnone size-large wp-image-19481" src="http://www.mscloud.be/wp-content/uploads/2017/05/subpolicies-1024x149.png" alt="" width="768" height="112" srcset="/wp-content/uploads/2017/05/subpolicies-1024x149.png 1024w, /wp-content/uploads/2017/05/subpolicies-300x44.png 300w, /wp-content/uploads/2017/05/subpolicies-768x112.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](http://www.mscloud.be/wp-content/uploads/2017/05/subpolicies.png)

&nbsp;

To test our new Azure Resource Policy lets deploy something in Canada.

[<img class="alignnone size-full wp-image-19491" src="http://www.mscloud.be/wp-content/uploads/2017/05/canada.png" alt="" width="469" height="498" srcset="/wp-content/uploads/2017/05/canada.png 469w, /wp-content/uploads/2017/05/canada-283x300.png 283w" sizes="(max-width: 469px) 100vw, 469px" />](http://www.mscloud.be/wp-content/uploads/2017/05/canada.png)

As you can see the deployment is being blocked by our Policy!

[<img class="alignnone size-large wp-image-19511" src="http://www.mscloud.be/wp-content/uploads/2017/05/locationerror-1024x493.png" alt="" width="768" height="370" srcset="/wp-content/uploads/2017/05/locationerror-1024x493.png 1024w, /wp-content/uploads/2017/05/locationerror-300x145.png 300w, /wp-content/uploads/2017/05/locationerror-768x370.png 768w, /wp-content/uploads/2017/05/locationerror-330x160.png 330w" sizes="(max-width: 768px) 100vw, 768px" />](http://www.mscloud.be/wp-content/uploads/2017/05/locationerror.png)

In the next blog post we will use the same PowerShell script but create and assign a policy to enforce a naming convention. So stay tuned!