---
id: 19678
title: Create a Web Application Monitor in opsmgr Part I
date: 2008-10-19T08:58:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2008/10/19/create-a-web-application-monitor-in-opsmgr.aspx
permalink: /create-a-web-application-monitor-in-opsmgr/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "3148"
  - "3148"
  - "3148"
  - "3148"
  - "3148"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Management Pack
  - manuals
  - Operations Manager 2007
  - opsmgr
  - scom
  - web application monitoring
---
At the moment I&#8217;m testing web application monitoring, service level dashboard, etc. So the upcoming posts will handle on how to set up a web application monitoring, how to configure the service level dashboard etc. 

The Web Application Monitor provides the synthetic transaction for the Service Level Dashboard. It monitors the Web application and then changes the health state of an object associated with the Web application, based on the results of the synthetic transaction. It is this change in health state that the Service Level Dashboard records and reports on. 

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="149" alt="petshop" src="http://scug.be/scom/files/2012/06/clip_image0027_thumb.jpg" width="198" border="0" />](http://scug.be/scom/files/2012/06/clip_image0027.jpg) 

&#160;

**To create a new Web Application Monitor** 

1. In the Operations Console, click the Authoring button. 

2. In the **Authoring** pane, click Management Pack Templates. 

3. Under Actions, click Add Monitoring Wizard. 

4. In the Add Monitoring Wizard, on the **Select Monitoring Type** page, click **Web Application**, and then click **Next**. 

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="215" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb.png" width="244" border="0" />](http://scug.be/scom/files/2012/06/image_2.png) 

5. On the **General Properties** page, do the following: 

> a. Type the **Name** for the object, such as **Petshop**. 

> b. Optionally, type a **Description** for the object. 

> c. From the list, click the management pack created in the previous step or click **New** to create a management pack. It is recommended to create one management pack per application, and group all transactions for a specific application into this management pack. 
> 
> [<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="215" alt="clip_image002" src="http://scug.be/scom/files/2012/06/clip_image002_thumb_414819FF.jpg" width="244" border="0" />](http://scug.be/scom/files/2012/06/clip_image002_5B1C502E.jpg)

Note&#160;&#160; Because the object type will be added to the specified management pack, only unsealed management packs are listed. For more information, see [Management Packs in Operations Manager 2007](http://technet.microsoft.com/en-us/library/bb309695.aspx). 

&#160;

6. Click **Next**. 

7. On the **Enter and Test Web Address** page, do the following: 

> a. Select **http://** or **https://** from the list.

> b. Type the URL for the Web application, such **as <http://petshop.com>**.

> c. Click **Test**.

> d. When the test succeeds, click **Next**.

Note&#160;&#160; It is possible to proceed through the wizard without this test succeeding. If the test returns an error, check the URL and click Details for more information. 

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="156" alt="clip_image002[9]" src="http://scug.be/scom/files/2012/06/clip_image002[9_5D005F00_thumb.jpg" width="177" border="0" />](http://scug.be/scom/files/2012/06/clip_image002[9].jpg) 

8. On the **Choose Watcher Nodes** page: 

> a. Select the watcher nodes on which you want to run the transaction. 

Note&#160;&#160; Operations Manager groups the results of the selected watcher nodes into a single monitor. To create separate monitors for different watcher nodes, you must create separate Web Application Monitors, even if they contain the same transaction. 

> b. Set the **Run this query every** value to the time that you want—the minimum is 30 seconds.

> c. Click **Next**. 
> 
> [<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="143" alt="clip_image002[11]" src="http://scug.be/scom/files/2012/06/clip_image002[11_5D005F00_thumb.jpg" width="162" border="0" />](http://scug.be/scom/files/2012/06/clip_image002[11].jpg)

9. On the **Summary** page, review the settings. You can select the **Configure Advanced Monitoring or Record a browser session** check box, and then click **Create**. If you select this check box, move to step 6 in the following procedure. 

Note&#160;&#160; Selecting Configure Advanced Monitoring or Record a browser session runs the Web Application Editor. For more information, see [Web Application Editor in Operations Manager 2007](/blogs/scom/archive/2008/10/19/add-a-recording-to-an-existing-web-application-object.aspx). 

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="152" alt="clip_image002[13]" src="http://scug.be/scom/files/2012/06/clip_image002[13_5D005F00_thumb.jpg" width="172" border="0" />](http://scug.be/scom/files/2012/06/clip_image002[13].jpg) 

grtz,

Alexandre Verkinderen

[http://scug.be/blogs](/blogs)