---
id: 19699
title: OpsMgr Management pack APC ISX Central Integration Management Pack
date: 2009-12-09T13:54:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2009/12/09/opsmgr-management-pack-apc-isx-central-integration-management-pack.aspx
permalink: /opsmgr-management-pack-apc-isx-central-integration-management-pack/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "4259"
  - "4259"
  - "4259"
  - "4259"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - APC
  - ISX Central
  - Management Pack
  - manuals
  - Operations Manager 2007
  - Opmsgr 2007 R2
  - opsmgr
  - opsmgr R2
---
This week I had to implement an APC management pack at a customer site and I will explain how to get it working. This customer is using APC to monitor and configure his _Uninterruptible power supply_ (UPS) infrastructure.

<img height="156" width="162" src="http://www.sourcewire.com/image.php?id=5690&s=l" /> 

&ldquo;

The APC InfraStruXure (ISX) Central is a network appliance that collects data from, and monitors status of, devices that provide data-center-critical infrastructure.  
The ISX Central Integration Management pack for Microsoft&rsquo;s System Center Operations Manager 2007 provides a tight integration between the physical infrastructure space for whichISX Central provides unprecedented visibility and control and the systems infrastructure space for which OpsMgr provides the same type of solution.

&ldquo;

The Management Pack integrates ISX Central through the new web services interface, available starting with version 5.1 of ISX Central. Make sure you install the ISX Central with a least version 5.1 that you can download from here [http://www.apc.com/products/resource/include/techspec\_index.cfm?base\_sku=SFISXC511](http://www.apc.com/products/resource/include/techspec_index.cfm?base_sku=SFISXC511 "http://www.apc.com/products/resource/include/techspec_index.cfm?base_sku=SFISXC511")&nbsp;

&nbsp;

To install the Management Pack, install the .msi package downloaded from the APC Web site (<http://www.apc.com/tools/download>) into an appropriate directory. The installation package consists of four  
files: this document, the sealed Management Pack (.mp), the optional Overrides Management Pack  
(.xml), and the registration utility (.exe).

&nbsp;

Steps to configure the APC management pack:

  1. Configure your ISX Central 
  2. Import your APC ISX management pack 
  3. Run the ISX Central Registration tool 
  4. Configure the run-as account 

&nbsp;

The registration utility is a tool that provides a user interface to set certain registry keys that are used by the Management Pack to perform the initial discovery of the InfraStruXure Central servers.

Start the ISX Central Registration tool that you can find in the management pack download folder. To add a new ISX Central registration, click Add. You will be asked to provide a name and FQDN for the ISX Central. The name can be any descriptive name.

[<img height="189" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_6D2C7639.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_18710D41.png)

The FQDN should be the IP address or FQDN of the ISX Central. Do not use a full URL here. The registry is updated immediately.

[<img height="186" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_25D72047.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_45F22D04.png)

Look in the registry.

All registry changes are made in the key:  
HKEY\_LOCAL\_MACHINESoftwareAPC MsScOpsMgrMpForIsxc  
&bull; The registered names appear as the REG_SZ values Name0&hellip;Name<n>  
&bull; The registered FQDNs appear as the REG_SZ values

[<img height="78" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_2BB6E542.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_04E8CF02.png)

Create a run as account and associate it with the run-as profile. O

[<img height="42" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_795311C2.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_0B9BD885.png)

Click next

[<img height="208" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_7B8F9A7E.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_59380505.png)

[<img height="207" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_6FF9DD3F.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_225DB0BF.png)

Click **New** which starts the **Create Run As Account Wizard** and opens the **General Properties** page

[<img height="205" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_686E6DD2.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_3AED4E0F.png)

create a new run as account.

[<img height="142" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_1D0ECA0E.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_242E0686.png)

Click Next

[<img height="216" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_715E0011.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_5CD8B093.png)

The Run As account should be created as a Simple Authentication Run As Account. Simple Authentication &#8211; any generic user name and password combination, for example, Web form, SQL authentication, or anything else that accepts user name and password.

[<img height="216" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_13B5958B.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_2D1D98C5.png)&nbsp;

The username and password should have access to the ISX Central.

[<img height="215" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_6F240806.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_3A83ABCB.png)

&ldquo;More secure&rdquo; means that when you associate the Run As account with a Run As profile, you have to provide the specific computer names that you want the Run As credentials distributed to. By positively identifying the destination computers, you can prevent the spoofing scenario that was described before.

[<img height="215" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_66C55411.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_2452B1DB.png)

[<img height="214" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_2D42441A.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_0D936A52.png)

In the **This Run As Account will be used to manage the following objects** area select **All targeted objects**

[<img height="143" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_61E2A055.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_6901DCCD.png)

[<img height="207" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_564CE316.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_369E094E.png)

[<img height="206" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_78A4788F.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_641F2911.png)

On the **Distribution** tab, in the **Selected computers:** area, click **Add** to open the **Computer Search** tool; **Search by computer name (Default)**, then type in the computer name. The computer name is the computer name where you have run the ISX Central Registration tool.

[<img height="244" width="239" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_26259853.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_71853C17.png)&nbsp;

[<img height="208" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_1A8FDB14.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_1F065BDB.png)

Enable the &ldquo;The InfraStruXure Central Registration discovery&rdquo; discovery. This discovery targets computers running Windows Server (i.e. the Microsoft.Windows.Server.Computer Operations Manager class) and looks for the registry keys that are written by the registration utility. This rule is disabled by default, which renders the Management Pack dormant on import.

[<img height="41" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_682C0794.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_13709E9C.png)

Enable the override for the computer object where the you have run the ISX Central Registration tool. Don&rsquo;t forget to enable the &ldquo;Agent Proxy&rdquo; option under Agent Properties > Security.

[<img height="244" width="243" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_5C964A55.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_331F7864.png)

After a while the ISX Central&nbsp; will be discovered and you will be able to monitor your UPS infrastructure!!

[<img height="150" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_23133A5E.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_03646096.png)

Hope this helps,

Alexandre Verkinderen
