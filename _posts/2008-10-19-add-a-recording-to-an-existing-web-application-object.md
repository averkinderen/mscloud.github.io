---
id: 19679
title: Add a recording to an existing Web Application object Part II
date: 2008-10-19T11:05:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2008/10/19/add-a-recording-to-an-existing-web-application-object.aspx
permalink: /add-a-recording-to-an-existing-web-application-object/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2677"
  - "2677"
  - "2677"
  - "2677"
  - "2677"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - end to end monitoring
  - Management Pack
  - manuals
  - Operations Manager 2007
  - opsmgr
  - scom
  - web application monitoring
---
**First you will have to create a web application monitor. See my previous post on how to** 

<a href="/blogs/scom/archive/2008/10/18/create-a-web-application-monitor-in-opsmgr.aspx" target="_blank">create a web application monitor in opsmgr.</a>

****&#160;

**To** add a recording to an existing Web Application object 

1. Open the Authoring pane. 

2. Expand **Management Pack Templates**, and then click **Web Application**. 

3. Select the object to which you want to add a recording. 

4. In the **Actions** pane, click **Edit Web application settings**. 

5. Select the request from the list where you want the recording to be inserted. Recordings are inserted after the request you select. 

6. In the **Actions** pane, click **Start capture**. Internet Explorer will open. If you receive an error message about third-party extensions being disabled, follow these steps: 

a. Click **Tools,** and then click **Internet Options**. 

b. Click the **Advanced** tab. 

c. Under **Browsing**, select **Enable third party browser extensions**. 

d. Close Internet Explorer, and then click **Start capture** to open the browser again. 

7. In the browser window, follow the actions you want to be monitored. For example, you might click some links or add a product to a shopping cart. 

&#160;

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="184" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_0C234D4D.png" width="244" border="0" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_47572918.png) 

     [  
](http://scug.be/scom/files/2012/06/clip_image002_2.jpg) 

When you have completed the recording, click **Stop** in the left pane of Internet Explorer. Or, in the **Acti****ons** pane, under **Run Now**, ****you can click **Run Test** to run the synthetic transaction immediately and see the results.

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="178" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_13EB3FEF.png" width="244" border="0" />](http://scug.be/scom/files/2012/06/image_0497DDE0.png) 

&#160;

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="184" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_1089A847.png" width="244" border="0" />](http://scug.be/scom/files/2012/06/image_137F0CFA.png) 

&#160;

Now we have to define our [health criteria&#160;](/blogs/scom/archive/2008/10/22/define-a-health-criteria-for-your-web-application-monitor.aspx) and a create the distributed application model to will drive the service level dashboard.

grtz,

Alexandre Verkinderen

[http://scug.be/blogs](/blogs)