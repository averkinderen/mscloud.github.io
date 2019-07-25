---
id: 600
title: OpsMgr Webconsole Runtime error “Server Error in ‘/’ Application”
date: 2009-12-02T20:07:29+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2009/12/02/opsmgr-webconsole-runtime-error-server-error-in-application.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1787"
  - "1787"
  - "1787"
  - "1787"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Consoles
  - Issue
  - Operations Manager 2007
  - Opmsgr 2007 R2
  - opsmgr
  - Opsmgr Console
  - opsmgr R2
  - webconsole
---
Just a little reminder that if you install the OpsMgr web console after the UI console has already been installed you will need to Copy the following files from the %Program Files%System Center Operations Manager 2007 directory to the %Program Files%System Center Operations Manager 2007Web ConsoleBin directory:

&#160;

  * Corgent.Diagramming.CommandResources.dll 
  * Corgent.Diagramming.CustomElements.dll 
  * Microsoft.ReportViewer.Common.dll 
  * Microsoft.ReportViewer.Webforms.dll 

&#160;

Otherwise you will get the following error when launching the webconsole:

[<img style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" border="0" alt="clip_image001[4]" src="http://scug.be/scom/files/2012/06/clip_image0014_thumb_5FE95CCA.jpg" width="244" height="184" />](http://scug.be/scom/files/2012/06/clip_image0014_281718A7.jpg)

&#160;

Hope this helps,

Alexandre Verkinderen
