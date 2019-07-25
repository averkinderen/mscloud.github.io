---
id: 2821
title: System Center Advisor Part 2 Installation
date: 2011-04-30T09:59:14+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2011/04/30/system-center-advisor-part-2-installation.aspx
permalink: /system-center-advisor-part-2-installation-2/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1832"
  - "1832"
  - "1832"
  - "1832"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Advisor
  - Cloud
  - system center
---
In the <a href="http://scug.be/blogs/scom/archive/2011/04/30/system-center-advisor-part-1-overview.aspx" target="_blank">previous blogpost</a> I gave you a short overview of System Center Advisor. Let’s have a look at the installation of System Center Advisor.

The installation is straight forward and easy.

## 

## Advisor System Requirements

At this moment Advisor will analyzes only the following workloads:

  * Windows Server 2008 and later: 
      * Active Directory 
      * Hyper-V Host 
      * General operating system 
  * SQL Server 2008 and later 
      * SQL Engine 

For SQL Server, the following 32-bit and 64-bit editions are supported for analysis:

  * SQL Server 2008 and 2008 R2 Enterprise 
  * SQL Server 2008 and 2008 R2 Standard 
  * SQL Server 2008 and 2008 R2 Workgroup 
  * SQL Server 2008 and 2008 R2 Web 
  * SQL Server 2008 and 2008 R2 Express 

In addition, the 32-bit edition of SQL Server is supported when running in the WOW64 implementation.

## &#160;

## Advisor Installation

&#160;

First logon <cite><a href="http://www.systemcenteradvisor.com">www.<b>systemcenteradvisor</b>.com</a> with your LiveID.</cite>

If you haven’t already installed an Advisor gateway the webconsole will prompt you to install one. 

[<img style="border-right-width: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="clip_image002_thumb" src="http://scug.be/scom/files/2012/06/clip_image002_thumb_thumb_7BF4209B.jpg" width="244" height="96" />](http://scug.be/scom/files/2012/06/clip_image002_thumb_247302B0.jpg) 

Follow the steps as described below:

First download the certificate and remember the location where you saved it. We will need this later on.

Next download the sofware.

[<img style="border-right-width: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="clip_image004_thumb" src="http://scug.be/scom/files/2012/06/clip_image004_thumb_thumb_61478482.png" width="244" height="206" />](http://scug.be/scom/files/2012/06/clip_image004_thumb_544DA471.png) 

In the directory where you downloaded the on-premise software, double-click AdvisorSetup.exe to launch the setup.

  1. Click **Next** on the Welcome page of the Setup wizard.</p> 
  2. Accept the license agreement, and then click **Next**.

  3. Enter the location where you want to install the on-premise software. By default, this location is %ProgramFiles%/System Center Advisor. Click **Next**.

  4. Select **Gateway** to install the gateway on this computer. You can also select **Agent** to install both the gateway and the agent. Click **Next**.

  5. A message is displayed about opening port 80 for communication with the agent. If you click **Yes**, the port is opened by the Setup program. If you click **No**, you are returned to the previous step. You cannot install the gateway without opening this port. 

[<img style="border-right-width: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="SNAG_Program-0253" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0253_thumb_6D68FEA9.png" width="244" height="187" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0253_6E416493.png)

On the Gateway Settings page, browse to the location where you downloaded the security certificate. Select the security certificate (RegistrationCert.pfx), and then click **OK**

[<img style="border-right-width: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="SNAG_Program-0254" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0254_thumb_36ABA3A5.png" width="244" height="187" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0254_3784098F.png)

If needed you can specify a web proxy so that the gateway can communicate with the Cloud service./

[<img style="border-right-width: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="SNAG_Program-0255" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0255_thumb_22B2110F.png" width="244" height="187" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0255_0E98F486.png)

The connection to Advisor is verified. If the connection can be verified, the gateway is registered with the Web service. If registering the gateway fails, you can continue with installation but will need to manually register the gateway. 

A new service will be added on your Windows Server that will handle the communication with the Advisor Cloud service.

[<img style="border-right-width: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="SNAG_Program-0258" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0258_thumb_6C60E8FF.png" width="244" height="13" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0258_1ABA6EAD.png)

And a new EventLog as well that will help you debug any communication issues

[<img style="border-right-width: 0px;padding-left: 0px;padding-right: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px;padding-top: 0px" border="0" alt="SNAG_Program-0267" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0267_thumb_71CF59A3.png" width="244" height="93" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/SNAG_Program-0267_00E6387E.png)

If you already had a SCOM agent installed it will now be configured to operate multi-homed and talk to two management groups:

[<img style="border-bottom: 0px;border-left: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top: 0px;border-right: 0px;padding-top: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_5722BD8A.png" width="244" height="144" />](http://scug.be/scom/files/2012/06/image_57FB2374.png)

&#160;

Once the gateway and the agents are installed they will show up in the webconsole but that can take some time:

[<img style="border-bottom: 0px;border-left: 0px;margin: 0px;padding-left: 0px;padding-right: 0px;border-top: 0px;border-right: 0px;padding-top: 0px" border="0" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_26AC3914.png" width="244" height="114" />](http://scug.be/scom/files/2012/06/image_285D04E8.png)

&#160;

Thanks,

Alexandre Verkinderen
