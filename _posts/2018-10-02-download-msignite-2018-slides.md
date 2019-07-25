---
id: 19867
title: Download MSIgnite 2018 slides
date: 2018-10-02T12:10:33+10:00
author: alexandre@verkinderen.com

guid: http://mscloud.be/?p=19867
permalink: /download-msignite-2018-slides/
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
  - "1718"
categories:
  - Azure
tags:
  - Azure
  - MSIgnite
  - powershell
---
Hi,

As Microsoft Ignite is now over I wanted to quickly download all Azure related slides. Luckily there are few PowerShell scripts available to do this but the best one I found is this one <https://gallery.technet.microsoft.com/Ignite-2016-Slidedeck-and-296df316> developed by Michel de Rooij.

I&#8217;ve noticed though that some of the default commands don&#8217;t work as expected. I would for example not get any slides if I run the script with the default parameters:

<pre class="lang:ps decode:true"> .\Get-IgniteSession.ps1 -DownloadFolder D:\Ignite -Keyword 'Azure'</pre>

[<img class="alignnone size-medium wp-image-19872" src="/wp-content/uploads/2018/10/2018-10-02_12-03-33-300x48.png" alt="" width="300" height="48" srcset="/wp-content/uploads/2018/10/2018-10-02_12-03-33-300x48.png 300w, /wp-content/uploads/2018/10/2018-10-02_12-03-33.png 360w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/10/2018-10-02_12-03-33.png)

But if I changed the Keyword parameter to Product it would work

<pre class="lang:ps decode:true"> .\Get-IgniteSession.ps1 -DownloadFolder D:\Ignite -Product 'Azure'</pre>

[<img class="alignnone size-medium wp-image-19873" src="/wp-content/uploads/2018/10/2018-10-02_12-05-40-300x36.png" alt="" width="300" height="36" srcset="/wp-content/uploads/2018/10/2018-10-02_12-05-40-300x36.png 300w, /wp-content/uploads/2018/10/2018-10-02_12-05-40.png 397w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/10/2018-10-02_12-05-40.png)

In my case I also had some PowerShell errors with the video&#8217;s which I didn&#8217;t really needed anyway. Luckily Michel added some really smart parameters into the script like the NoVideos switch.

<pre class="lang:ps decode:true "> .\Get-IgniteSession.ps1 -DownloadFolder D:\Ignite -Product 'Azure' -NoVideos</pre>

I know what I&#8217;m going to do the next couple of days 🙂

[<img class="alignnone wp-image-19868 size-large" src="/wp-content/uploads/2018/09/2018-09-30_9-24-58-1024x406.png" alt="" width="768" height="305" srcset="/wp-content/uploads/2018/09/2018-09-30_9-24-58-1024x406.png 1024w, /wp-content/uploads/2018/09/2018-09-30_9-24-58-300x119.png 300w, /wp-content/uploads/2018/09/2018-09-30_9-24-58-768x305.png 768w, /wp-content/uploads/2018/09/2018-09-30_9-24-58.png 1585w" sizes="(max-width: 768px) 100vw, 768px" />](/wp-content/uploads/2018/09/2018-09-30_9-24-58.png)

Thanks,

Alex
