---
id: 19798
title: How to use Azure CDN for WordPress
date: 2018-01-30T09:50:19+10:00
author: alexandre@verkinderen.com

guid: http://mscloud.be/?p=19798
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
  - "5472"
categories:
  - Azure
tags:
  - Azure
  - CDN
  - Wordpress
---
In this blogpost I will show you how you can use Azure CDN to improve the performance of your WordPress site. I’m running WordPress for my blog and have a lot of static content. All my blog post, once written and published will not change and remain the same year after year. This is a lot of static content that could be cached on Azure CDN. The Azure Content Delivery Network (CDN) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users. For a full list of Azure CDN POP locations have a look <a href="https://docs.microsoft.com/en-us/azure/cdn/cdn-pop-locations" target="_blank" rel="noopener">here</a>.  It really only takes a couple of minutes to deploy, it’s super easy and basically maintains itself once the configuration is done.

To use Azure CDN for your WordPress site you will need to follow these steps:

  1. Install a WordPress plugin that supports Azure CDN like <a href="https://en-au.wordpress.org/plugins/wp-super-cache/" target="_blank" rel="noopener">wp-super cache</a>.
  2. Deploy Azure CDN in your Azure subscription
  3. Configure the WordPress plugin to use Azure CDN

## 1) Install WP-super Cache


## 2) Deploy Azure CDN in your Azure subscription

Create CDN profile:  From NEW, search for CDN

[<img style="margin: 0px; display: inline; background-image: none;" title="cdn" src="http://mscloud.be/wp-content/uploads/2017/11/cdn_thumb.png" alt="cdn" width="244" height="121" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/cdn.png)

Create CDN Endpoint:  From the CDN profile, click “+Endpoint” to add an endpoint, choose the web site for Origin hostname, e.g.

[<img style="margin: 0px; display: inline; background-image: none;" title="cdn1" src="http://mscloud.be/wp-content/uploads/2017/11/cdn1_thumb.png" alt="cdn1" width="190" height="244" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/cdn1.png)

Because I like things to be nice and clean all the way, I registered a custom domain name too so that all my cached files would be available through a custom name: cdn.mscloud.be. You will then need to add this custom name to your DNS provider

[<img style="margin: 0px; display: inline; background-image: none;" title="cdnconfig" src="http://mscloud.be/wp-content/uploads/2017/11/cdnconfig_thumb.png" alt="cdnconfig" width="125" height="244" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/cdnconfig.png)[<img style="margin: 0px; display: inline; background-image: none;" title="customdomain" src="http://mscloud.be/wp-content/uploads/2017/11/customdomain_thumb.png" alt="customdomain" width="90" height="244" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/customdomain.png)

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/11/image_thumb-15.png" alt="image" width="244" height="21" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/image-15.png)

Once Azure CDN is deployed you can manage and see some reports here [https://cdn.windowsazure.com/](https://cdn.windowsazure.com/ "https://cdn.windowsazure.com/")

## 3) Configure the WordPress plugin to use Azure CDN

The last step is to tell our WordPress site to use Azure CDN. If you have WP Super Cache plugin installed on your WordPress site, you can use WP Super Cache to integrate with Azure CDN:

Edit from WP Super Cache “Settings”, select “CDN” tab, put the URL of Azure CDN endpoint in “Off site URL”, save the change.

[<img style="display: inline; background-image: none;" title="enablecdn" src="http://mscloud.be/wp-content/uploads/2017/11/enablecdn_thumb.png" alt="enablecdn" width="244" height="157" border="0" />](http://mscloud.be/wp-content/uploads/2017/11/enablecdn.png)

That&#8217;s it! As you can see it is really easy and straight forward to use Azure CDN for your WordPress website!

&nbsp;

Hope this helps,

Alexandre
