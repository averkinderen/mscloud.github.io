---
id: 251
title: CloudCruiser unable to connect to usage server
date: 2014-12-21T21:22:12+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://www.mscloud.be/?p=251
permalink: /cloudcruiser-unable-to-connect-to-usage-server/
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
  - "2463"
  - "2463"
  - "2463"
categories:
  - WAP
tags:
  - Chargeback
  - Cloud
  - Cloudcruiser
  - WAP
---
Hi,

Last week when installing [Cloudcruiser](http://www.cloudcruiser.com/) for my lab environment I encountered an issue when trying to connect to my WAP usage server. After a few days of searching I gave up and emailed CloudCruiser support and this was their response:

> Make sure you are using Java 7 as per the installation instructions. CCX does not support Java 8 yet and others attempting to install without Java 7 have reported being stuck at this point.

I uninstalled Java 8, installed java version 7 and voila! It worked! I could finally start showcasing the power of Financial management for Clouds:

[<img class="alignnone size-medium wp-image-231" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2014/12/image-300x264.png" alt="image.png" width="300" height="264" srcset="/wp-content/uploads/2014/12/image-300x264.png 300w, /wp-content/uploads/2014/12/image-768x676.png 768w, /wp-content/uploads/2014/12/image.png 872w" sizes="(max-width: 300px) 100vw, 300px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2014/12/image.png)

&nbsp;

If you need more information on how to install Cloudcruiser from the beginning read Christopher’s blog post <http://scug.be/christopher/2014/02/28/windows-azure-pack-cloud-cruiser-installation/>

Thanks,

Alexandre Verkinderen