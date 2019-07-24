---
id: 519
title: Microsoft.interop.security.azroles.dll error when installing opsmgr
date: 2008-08-25T14:20:21+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2008/08/25/microsoft-interop-security-azroles-dll-error-when-installing-opsmgr.aspx
permalink: /microsoft-interop-security-azroles-dll-error-when-installing-opsmgr/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1380"
  - "1380"
  - "1380"
  - "1380"
  - "1380"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Issue
  - Operations Manager 2007
  - opsmgr
  - scom
---
Yesterday I wanted to install my second management server on a windows 2003 R2 SP2 machine. I installed all the requirements and ran the prerequisite checker.

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="213" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/Microsoft.i.dllerrorwheninstallingopsmgr_E5B4/image_thumb.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/Microsoft.i.dllerrorwheninstallingopsmgr_E5B4/image_2.png) 

&nbsp;

I was really astonished! It was the first time I saw this error and didn&#8217;t understand it!

&nbsp;

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="168" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/Microsoft.i.dllerrorwheninstallingopsmgr_E5B4/image_thumb_1.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/Microsoft.i.dllerrorwheninstallingopsmgr_E5B4/image_4.png) 

&nbsp;

[http://support.microsoft.com/default.aspx?scid=KB;[LN];937292](http://support.microsoft.com/default.aspx?scid=KB;[LN];937292 "http://support.microsoft.com/default.aspx?scid=KB;[LN];937292")

&nbsp;

This problem occurs if the primary interoperability assembly (Microsoft.interop.security.azroles.dll) is no longer registered in the global assembly cache after you install Microsoft Windows Server 2003 with Service Pack 1 or Windows Server 2003 with Service Pack 2.

To resolve this problem in Windows Server 2003 with Service Pack 2, re-register the primary interoperability assembly in the global assembly cache.  
To do this, follow these steps:

  1. Click **Start**, click **Run**, type <kbd>cmd</kbd> , and then click **OK**. 
      * At the command prompt, type the following commands. Press ENTER after you type each command. 
      * <kbd>cd %windir%Microsoft.NETAuthMan1.2</kbd> 
          * <kbd>azrlreg register Microsoft.interop.security.azroles.dl</kbd></ul> 
          * <kbd></kbd>run the prerequisite checker again and everything is green now!</ol> 
        &nbsp;
        
        Greetz,
        
        Alexandre Verkinderne
        
        <http://scug.be/blogs/scom>