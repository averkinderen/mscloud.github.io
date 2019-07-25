---
id: 2611
title: Cumulative Update 2 for OpsMgr installation
date: 2010-05-01T12:28:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2010/05/01/cumulative-update-2-for-opsmgr-installation.aspx
permalink: /cumulative-update-2-for-opsmgr-installation/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2201"
  - "2201"
  - "2201"
  - "2201"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Cumulative Update
  - Issue
  - KB
  - Management Pack
  - Operations Manager 2007
  - Opmsgr 2007 R2
  - opsmgr
  - opsmgr R2
  - R2
---
High Level overview steps:

  1. Root Management Server</p> 
  2. Manual update of the Operations Manager database together with the included stored procedure file that is discussed later

  3. Manual import of the Management Pack library that is discussed later

  4. Secondary Management Servers

  5. Gateway Servers

  6. Deploy the agent update to the agents that used a discovery-based installation

  7. Operations console role computers  
    **Note** Select the **Run Server Update** option from the **Software Update** dialog box.

  8. Web Console server role computers

  9. Audit Collection Services role computers

 10. Apply the agent update to manually installed agents

**Note** **To run this file on a computer that is running Windows Server 2008, you must use an elevated command prompt. An elevated command prompt is a command prompt that was started by using the** **Run as Administrator** **option. If you do not run this Windows-based installer file under an elevated command prompt, the System Center Operations Manager 2007 Software Update splash screen does not allow for the installation of the hotfix.**

Download the corresponding CU2.MSI file <http://www.microsoft.com/downloads/details.aspx?FamilyID=61714687-668a-46e4-b127-ad8519594351&displaylang=en> and launch it:

[<img height="181" width="244" src="http://scug.be/scom/files/2012/06/clip_image001_thumb_593EF743.png" alt="clip_image001" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image001_59AB2A38.png)****

The only thing you can do here is to accept the license agreement. Don&rsquo;t forget to read it&hellip;.

[<img height="199" width="244" src="http://scug.be/scom/files/2012/06/clip_image002_thumb_4A281869.png" alt="clip_image002" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image002_1CA6F8A6.png)****

[<img height="199" width="244" src="http://scug.be/scom/files/2012/06/clip_image003_thumb_09199905.png" alt="clip_image003" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image003_429CA8FC.png)****

This is the installation folder where the files will be stored that we will need for the manual operations that must be performed after you update the RMS

[<img height="199" width="244" src="http://scug.be/scom/files/2012/06/clip_image004_thumb_0121F6A3.png" alt="clip_image004" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image004_3AA5069A.png)****

[<img height="199" width="244" src="http://scug.be/scom/files/2012/06/clip_image005_thumb_4732B3B6.png" alt="clip_image005" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image005_0E8809A9.png)****

[<img height="193" width="244" src="http://scug.be/scom/files/2012/06/clip_image007_thumb_3411870A.jpg" alt="clip_image007" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image007_74B3D379.jpg)****

[<img height="183" width="244" src="http://scug.be/scom/files/2012/06/clip_image008_thumb_7779886C.png" alt="clip_image008" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image008_57CAAEA4.png)****

It&rsquo;s going to start and stop the opsmgr services. Don&rsquo;t worry about it

[<img height="186" width="244" src="http://scug.be/scom/files/2012/06/clip_image009_thumb_3260BB36.png" alt="clip_image009" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image009_64C48EB5.png)****

[<img height="157" width="244" src="http://scug.be/scom/files/2012/06/clip_image010_thumb_1C2A9FE4.png" alt="clip_image010" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image010_116D488F.png)****

[<img height="157" width="244" src="http://scug.be/scom/files/2012/06/clip_image011_thumb_748423B9.png" alt="clip_image011" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image011_49ABBFA7.png)****

Also don&rsquo;t panic if you see event ID&rsquo;s 29104. That&rsquo;s normal during the upgrade process.

[<img height="157" width="244" src="http://scug.be/scom/files/2012/06/clip_image012_thumb_2EFF238E.png" alt="clip_image012" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image012_6162F70D.png)****

It can take a while but finally my RMS is updated

[<img height="185" width="244" src="http://scug.be/scom/files/2012/06/clip_image013_thumb_58FF21B6.png" alt="clip_image013" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image013_2773B421.png)****

Just like with the CU1 I chose to not restart the server automatically. When you click no you allow the hotfix installation to finish all his post-processes. Check if the file versions has been updated and only then reboot the server.

[<img height="53" width="244" src="http://scug.be/scom/files/2012/06/clip_image015_thumb_05A7DB90.jpg" alt="clip_image015" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image015_7841C889.jpg)

I can see that the files have been updated

[<img height="92" width="244" src="http://scug.be/scom/files/2012/06/clip_image016_0C5AE513.png" alt="clip_image016" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://blogs.technet.com/blogfiles/kevinholman/WindowsLiveWriter/OpsMgr2007R2CU2rolluphotfixshipsandmyexp_85DA/image_8.png)****

****

**Manual operations that must be performed after you update the Root Management Server**

**Note** **You do not have to repeat the DiscoveryEntitySProcs.SQL installation if you have previously installed Cumulative Update 1 for System Center Operations Manager 2007 R2.**

As in my environment I already applied the CU 1 I can skip this step.

**Import updated management packs**

This updated management pack is located in the **ManagementPacks** folder of the package installation.

Microsoft.SystemCenter.DatawareHouse.Report.Library.mp

Now you need to upgrade the other opsmgr components as well. I don&rsquo;t have other MS servers in my lab environment so I&rsquo;m going to skip this step.

**Remember to upgrade one MS server at a time.** 

[<img height="193" width="244" src="http://scug.be/scom/files/2012/06/clip_image018_thumb_644835F3.jpg" alt="clip_image018" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image018_0BEEB21E.jpg)

Last step is to approve the pending agents

[<img height="89" width="244" src="http://scug.be/scom/files/2012/06/clip_image020_thumb_29ECC012.jpg" alt="clip_image020" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image020_35827D51.jpg)

[<img height="244" width="233" src="http://scug.be/scom/files/2012/06/clip_image021_thumb_33657E88.png" alt="clip_image021" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](http://scug.be/scom/files/2012/06/clip_image021_1BAE4722.png)

Manually installed agents should be upgraded manually. Or you can easily create a SCCM package and deploy that.

If you have not already done so, create a new view that shows the agent patch list as described on Kevin Holmans blog: <http://blogs.technet.com/kevinholman/archive/2008/06/24/how-do-i-know-which-hotfixes-have-been-applied-to-which-agents.aspx>

That&rsquo;s it!

Pretty easy upgrade

Thanks,  
Alexandre Verkinderen
