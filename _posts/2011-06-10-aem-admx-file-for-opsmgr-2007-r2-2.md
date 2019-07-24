---
id: 2911
title: AEM ADMX File for OpsMgr 2007 R2
date: 2011-06-10T06:31:35+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2011/06/10/aem-admx-file-for-opsmgr-2007-r2.aspx
permalink: /aem-admx-file-for-opsmgr-2007-r2-2/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2015"
  - "2015"
  - "2015"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - ADM
  - ADMX
  - AEM
  - GPO
  - opsmgr
  - opsmgr R2
---
Last week I was at a customer to implement AEM.

The customer is fully on Windows 2008 R2 and Windows 7 and only want to use ADMX files and not ADM files to configure his GPO’s. And here is the issue….When running the AEM configuration wizard the settings are stored as an ADM file not an ADMX file. 

[<img style="border-bottom: 0px;border-left: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top: 0px;border-right: 0px;padding-top: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_2516E0F0.png" width="244" height="214" />](http://scug.be/scom/files/2012/06/image_3499F2BF.png)

Note that the ADM file format that the wizard provides will work on Windows 7 and W2K8 R2 but some companies have new policies in the place which require them to only use ADMX file types and so this is the stop gap solution for now. 

Luckily the product team just release yesterday an ADMX file for OpsMgr 2007 R2!! [http://blogs.technet.com/b/momteam/archive/2011/06/08/aem-admx-file-for-opsmgr-2007-r2.aspx](http://blogs.technet.com/b/momteam/archive/2011/06/08/aem-admx-file-for-opsmgr-2007-r2.aspx "http://blogs.technet.com/b/momteam/archive/2011/06/08/aem-admx-file-for-opsmgr-2007-r2.aspx")&#160; Notice that this has been through very limited testing but it worked like a charm in my customer environment!

So a big thank you to the product team and especially Satya to help me out with this.

[<img style="border-bottom: 0px;border-left: 0px;padding-left: 0px;padding-right: 0px;border-top: 0px;border-right: 0px;padding-top: 0px" border="0" alt="thank-you" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/thank-you_thumb_3E9E6E1D.jpg" width="165" height="133" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/thank-you_43ED54CE.jpg)

Thanks,  
Alexandre Verkinderen