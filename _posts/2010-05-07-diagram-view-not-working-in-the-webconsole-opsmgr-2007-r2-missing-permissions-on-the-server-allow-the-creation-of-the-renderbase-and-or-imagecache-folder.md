---
id: 623
title: 'Diagram view not working in the webconsole OpsMgr 2007 R2: “missing permissions on the server allow the creation of the RenderBase and/or ImageCache folder”'
date: 2010-05-07T12:50:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2010/05/07/diagram-view-not-working-in-the-webconsole-opsmgr-2007-r2-missing-permissions-on-the-server-allow-the-creation-of-the-renderbase-and-or-imagecache-folder.aspx
permalink: /diagram-view-not-working-in-the-webconsole-opsmgr-2007-r2-missing-permissions-on-the-server-allow-the-creation-of-the-renderbase-and-or-imagecache-folder/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1797"
  - "1797"
  - "1797"
  - "1797"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - IIS
  - Issue
  - Operations Manager 2007
  - Opmsgr 2007 R2
  - opsmgr
  - opsmgr R2
  - webconsole
---
Today I ran into the following problem: I was unable to access diagram views from the webconsole. Every other view like a state view, performance view, alert view etc was working but not the diagram view:

&nbsp;

[<img height="131" width="244" src="http://scug.be/scom/files/2012/06/clip_image002_thumb_3C9CA96D.jpg" alt="clip_image002" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image002_35E99FEA.jpg)

Likely this is due to missing permissions on the server allow the creation of the RenderBase and/or ImageCache folder or the ability to create files in these folders. Either add the permissions for the anonymous INET user to write to the root folder, or create the RenderBase and/or ImageCache folder and in the root of the web application and add write access to these folders.

&nbsp;

As you can see the temp folder is empty

&nbsp;

[<img height="94" width="244" src="http://scug.be/scom/files/2012/06/clip_image004_thumb_7547537A.jpg" alt="clip_image004" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image004_636ABFAD.jpg)

you need to give the group called IIS_IUSRS read and write permissions to the root folder of the webconsole

[<img height="171" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_22C8733E.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_6E281702.png)

once done you will see the following files being created in the temp folder:

[<img height="98" width="244" src="http://scug.be/scom/files/2012/06/clip_image005_thumb_09607004.png" alt="clip_image005" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image005_34A5070B.png)

and now the final test!

[<img height="121" width="244" src="http://scug.be/scom/files/2012/06/clip_image007_thumb_141DC759.jpg" alt="clip_image007" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image007_6D4FB118.jpg)

woohoo it&#8217;s working! 🙂

&nbsp;

And now you will see a PNG file in the temp folder for every diagram view you open. That&rsquo;s why you need to modify the rights so that the group IIS_USRS can add those PNG files to the temp folder.

[<img height="121" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_13B19464.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_3AEBDD99.png)

I don&rsquo;t think this is very efficient. Image a NOC with 10 guys consulting the webconsole and each one of them opens 2 views and with 4 levels each then you will 80 PNG files in the temp folder!! But that&rsquo;s a total different discussion 🙂

&nbsp;

Hope this helps,

Alexandre Verkinderen