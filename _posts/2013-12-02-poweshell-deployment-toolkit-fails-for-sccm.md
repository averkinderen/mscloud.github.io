---
id: 714
title: Poweshell Deployment Toolkit fails for SCCM
date: 2013-12-02T06:05:00+10:00
author: alexandre@verkinderen.com

guid: http://scug.be/scom/?p=714
permalink: /poweshell-deployment-toolkit-fails-for-sccm/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1858"
  - "1858"
  - "1858"
  - "1858"
categories:
  - Powershell
  - Uncategorized
tags:
  - pdt
  - powershell
  - SCCM
  - sql
---
&nbsp;

I kept getting errors on the automatic deployment of SCCM with the PDT toolkit. The thing is that SCCM cannot work with Dynamic ports as described here:

So to fix this just change the SQL port in the to a fix port like shown below:

[<img style="padding-top: 0px; padding-left: 0px; margin: 0px; padding-right: 0px; border-width: 0px;" title="image" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2013/11/image_thumb1.png" width="644" height="149" border="0" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2013/11/image11.png)

Normally PDT is going to verify if all the SQL settings are defined correctly during the pre-install validation except for this one. So if you want PDT to verify that the SCCM instance is not set to a dynamic port you can add:

[xml]<SQL>  
<Port>True</Port>  
</SQL>[/xml]

…to the <Validation> section of the SC DB role in the variable.xml file

Thanks for <a href="http://blogs.technet.com/b/privatecloud/" target="_blank">Rob Willis</a> to help me with this.

Alex
