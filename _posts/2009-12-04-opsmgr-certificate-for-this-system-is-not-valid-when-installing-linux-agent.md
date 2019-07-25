---
id: 19698
title: 'OpsMgr : Certificate for this system  is not valid when installing Linux agent'
date: 2009-12-04T15:15:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2009/12/04/opsmgr-certificate-for-this-system-is-not-valid-when-installing-linux-agent.aspx
permalink: /opsmgr-certificate-for-this-system-is-not-valid-when-installing-linux-agent/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2445"
  - "2445"
  - "2445"
  - "2445"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Agent
  - Agents
  - certificates
  - Cross Platform
  - Issue
  - linux
  - opsmgr
  - opsmgr R2
---
Today I ran into some Linux agent deployment issues. I needed to monitor about 20 Redhat Machines . In such an environment environment, Kerberos authentication is not possible. Therefore, certificates are used between the management server and the UNIX-based or Linux-based computers.

[<img height="109" width="135" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/windowstolinux_thumb_6C427B98.jpg" alt="windows-to-linux" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/windowstolinux_37A21F5D.jpg)

First if you have some Cross-platform agent deployment issues please have a look at the following blog posts:

  * [http://wmug.co.uk/blogs/aquilaweb/archive/2009/07/21/opsmgr-r2-xplat-agent-deployment-field-notes.aspx](http://wmug.co.uk/blogs/aquilaweb/archive/2009/07/21/opsmgr-r2-xplat-agent-deployment-field-notes.aspx "http://wmug.co.uk/blogs/aquilaweb/archive/2009/07/21/opsmgr-r2-xplat-agent-deployment-field-notes.aspx")
  * [http://wmug.co.uk/blogs/aquilaweb/archive/2009/09/02/more-opsmgr-x-plat-notes.aspx](http://wmug.co.uk/blogs/aquilaweb/archive/2009/09/02/more-opsmgr-x-plat-notes.aspx "http://wmug.co.uk/blogs/aquilaweb/archive/2009/09/02/more-opsmgr-x-plat-notes.aspx")
  * [http://wmug.co.uk/blogs/aquilaweb/archive/2009/07/22/enable-opsmgr-module-logging.aspx](http://wmug.co.uk/blogs/aquilaweb/archive/2009/07/22/enable-opsmgr-module-logging.aspx "http://wmug.co.uk/blogs/aquilaweb/archive/2009/07/22/enable-opsmgr-module-logging.aspx")
  * <http://blog.xplatxperts.com/xplat-xperts/2009/08/opsmgr-cross-platform-discovery-errors.html>

&nbsp;

Ok, let&rsquo;s start!

So after making sure I had all the pre-requisites needed to deploy an Linux agent I launched the discovery wizard

[<img height="215" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_6BD648A3.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_65233F20.png)

But my agent installation failed because the certificate could not be signed.

[<img height="158" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_2076A4DF.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_4091B19C.png)

The certificate signing process does the following:

<table cellpadding="0" cellspacing="0" border="1">
  <tr>
    <td width="295" valign="top">
      Operations Manager retrieves the certificate from the agent, signs the certificate, deploys the certificate back to the agent, and then restarts the agent.
    </td>
  </tr>
</table>

[<img height="184" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_2DDCB7E5.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_75320DD7.png)

For an unknow reason my certifcate was not signed and trusted.

&nbsp;I also got the following error in my event log:

Unexpected ScxCertLibException: Unable to open root store  
; input data is: &#8212;&#8211;BEGIN CERTIFICATE&#8212;&#8211;  
MIIDHjCCAgYCAQEwDQYJKoZIhvcNAQEFBQAwZjEYMBYGA1UEAxMPU0NYLUNlcnRp  
ZmljYXRlMTAwLgYDVQQMEydTQ1g2MzMzNzZEMi1FM0UyLTRmMzEtODQ2MS1EMDky

[<img height="158" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_37387D19.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_30857396.png)

&nbsp;

To solve this problem you need to sign the certificate on your OpsMgr server following this procedure:

&nbsp;Download and install [Winscp](http://winscp.net/eng/docs/lang:nl) on your OpsMgr server.

&nbsp;Start Winscp and connect to your Linux machine

[<img height="169" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_4BBDCC97.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_491510E6.png)

Click yes

[<img height="92" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_60431C15.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_728BE2D7.png)

Browse to /etc/opt/microsoft/scx/ssl

[<img height="138" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_7F85C2E8.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_07113256.png)

Copy the key scx-host-<hostname>.pem&nbsp; to your opsmgr server.

[<img height="144" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_3D81E458.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_6D3CFC26.png)

Open the command prompt on your OpsMgr server and change directories to the location where you copied the certificate. Type the command

&ldquo;scxcertconfig -sign scx-host-<hostname>.pem scx_new.pem&rdquo;

and then press ENTER. This command will self-sign your certificate (scx-host-<hostname>.pem) and then save the new certificate.

[<img height="194" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_4AE7F75E.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_16479B23.png)

Rename your scx_new.pem file with scx-host-<hostname>.ad.pem and replace the original file on your linux server with this file.

[<img height="144" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_4A7BC469.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_5CC48B2B.png)

Connect to your Linux server with putty

[<img height="64" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_73F2965A.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_1F372D62.png)

and type scxadmin &ndash;restart

[<img height="43" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_7AA59FDD.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_53D7899D.png)

This step is very important! If you don&rsquo;t restart the scxadmin the discovery wizard will still complain about the certificate not being signed!!

&nbsp;

Now close your discovery wizard and re launch it.

[<img height="203" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_335049EB.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_459910AD.png)

The Discovery Wizard discovers the computer and tests to see that the certificate is valid. If the Discovery Wizard verifies that the computer can be discovered and that the certificate is valid, the Discovery Wizard adds the newly discovered computer to the Operations Manager database.Almost immediately you will get a message saying the agent is successfully signed and installed:

[<img height="210" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_47D59969.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/image_6F0FE29E.png)

&nbsp;

Hope this helps,

Alexandre Verkinderen
