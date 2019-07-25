---
id: 19942
title: Azure API Management Consumption Tier
date: 2019-01-17T14:16:32+10:00
author: alexandre@verkinderen.com

guid: http://mscloud.be/?p=19942
permalink: /azure-api-management-consumption-tier/
sc_member_order:
  - "0"
bpxl_standard_excerpt_home:
  - "0"
bpxl_standard_single_hide:
  - "0"
bpxl_image_excerpt_home:
  - "0"
bpxl_image_single_hide:
  - "0"
bpxl_audio_excerpt_home:
  - "0"
bpxl_audio_single_hide:
  - "0"
bpxl_video_excerpt_home:
  - "0"
bpxl_video_single_hide:
  - "0"
bpxl_link_excerpt_home:
  - "0"
bpxl_link_single_hide:
  - "0"
bpxl_gallery_excerpt_home:
  - "0"
bpxl_gallery_single_hide:
  - "0"
bpxl_status_excerpt_home:
  - "0"
bpxl_status_single_hide:
  - "0"
bpxl_singlerelated:
  - "0"
post_views_count:
  - "1196"
categories:
  - Azure
tags:
  - API
  - API Management
  - Azure
---
Microsoft has announced a new<a href="https://azure.microsoft.com/en-us/blog/announcing-azure-api-management-for-serverless-architectures/" target="_blank" rel="noreferrer noopener">&nbsp;Azure API Management Consumption tier</a>. This new tier aligns with serverless architecture principles that includes automated scaling, built-in high availability and requires no infrastructure to provision or manage.&nbsp;

Traditionally, Azure API Management has been deployed through a&nbsp;<a rel="noreferrer noopener" href="https://azure.microsoft.com/en-us/pricing/details/api-management/" target="_blank">scale unit approach</a>&nbsp;that is measured hourly. This approach results in billing events being accrued, irrespective of whether the API gateway is processing requests. By contrast, the new consumption tier is **only billed based on usage.**

While the underlying API Management service components remain the same across existing and consumption tiers, some additional features are provided by the new tier. It is important to note, there are some key differences with the consumption based tier as it does not provide an built-in cache, developer portal, management portal, disaster recovery strategies (i.e. backup/restore), configuration into Git, Azure Active Directory integration, Virtual Network support, multi-region deployment and has&nbsp;<a href="https://docs.microsoft.com/en-us/azure/azure-subscription-service-limits#api-management-limits" target="_blank" rel="noreferrer noopener">usage limits</a>. 

The following table provides a comparison of features between the new and the traditional tiers.&nbsp;<figure class="wp-block-image">

<img src="/wp-content/uploads/2019/01/api-consumption-tier-1024x603.png" alt="" class="wp-image-19944" srcset="/wp-content/uploads/2019/01/api-consumption-tier-1024x603.png 1024w, /wp-content/uploads/2019/01/api-consumption-tier-300x177.png 300w, /wp-content/uploads/2019/01/api-consumption-tier-768x452.png 768w, /wp-content/uploads/2019/01/api-consumption-tier.png 1068w" sizes="(max-width: 1024px) 100vw, 1024px" /> <figcaption>  
_Image source:&nbsp;<a rel="noreferrer noopener" href="https://azure.microsoft.com/en-us/blog/announcing-azure-api-management-for-serverless-architectures/" target="_blank">https://azure.microsoft.com/en-us/blog/announcing-azure-api-management-for-serverless-architectures/</a>_ </figcaption></figure> 

Further, the new tier provides two additional features of Bring Your Own Cache (BYOC) and flexible API Key subscriptions. 

### Bring Your Own Cache

The BYOC feature allows for the use of an&nbsp;<a href="https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-cache-external" target="_blank" rel="noreferrer noopener">externally provisioned Redis-compatible cache</a> that is especially beneficial by providing more cache data capacity than the API Management tier allows, and prevents the cache being cleared during API Management updates. Caching reduces the load on backend systems when data is frequently requested but does not regularly change. It also has the benefit of reducing costs associated with requests to the backend services.

### API Key Subscriptions

The API Key subscriptions have a more flexible option that allows standalone subscriptions to exist that are not associated with a user. Keys can also be created to grant access to an API or _all APIs_ within an API Management instance without first having to associate them to a _Product_. Using the _all APIs_ subscription option provides for an even more straightforward method for testing and debugging within the Test panel of the API Management.

### Conclusion

The new consumption tier will not be suitable for every situation but allows for smaller applications or services to deploy an entry-level model of the API Management.

Please stayed tuned for some more API management blogs in the near future.

Written by Peter Bosen and Alexandre Verkinderen (CO4 Team)
