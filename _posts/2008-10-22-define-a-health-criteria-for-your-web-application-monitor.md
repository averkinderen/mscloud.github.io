---
id: 533
title: Define a Health Criteria for your web application Monitor Part III
date: 2008-10-22T21:52:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2008/10/22/define-a-health-criteria-for-your-web-application-monitor.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1960"
  - "1960"
  - "1960"
  - "1960"
  - "1960"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - end to end monitoring
  - manuals
  - Operations Manager 2007
  - opsmgr
  - scom
  - service level dashboard
  - web application monitoring
---
W&#8217;re almost at the end! 🙂 Only 3 steps left. First we have to define a healt criteria for our web appliction and after that we can [create our distributed appliction](/blogs/scom/archive/2008/10/22/creating-the-distributed-application-models-to-drive-the-service-level-dashboard.aspx) that will drive ou service level dashboard.

&#160;

Use the Web Application Editor to choose what conditions will cause an error or warning during a synthetic transaction. For the Service Level Dashboard, an error is equivalent to an availability exception, and a warning is equivalent to a performance exception. Availability exceptions will also affect performance reporting. You can also choose to generate an alert when the status changes. For example, if your transaction includes a request to a specific Web page, you can choose to generate an alert if the page is unavailable. This is done by changing the health status of the transaction when the HTTP status code is 404. 

Synthetic transactions are created by recording a Web site or by manually creating requests. For more information about recording a Web site, see [How to Capture a Web Application Recording in Operations Manager 2007](/blogs/scom/archive/2008/10/18/create-a-web-application-monitor-in-opsmgr.aspx). For more information about manually creating or editing individual requests, see 

[How to Create or Edit a Request in Operations Manager 2007.](/blogs/scom/archive/2008/10/19/add-a-recording-to-an-existing-web-application-object.aspx)

**To set health criteria for a request in a Web monitoring session** 

1. Open the Authoring pane. 

2. Expand **Management Pack Templates**, and then click **Web Application**. 

3. Select the object you want to edit, and then click **Edit Web application settings**. 

4. In the **Request Details** pane, you can set criteria to generate an error or warning health state for the request. For example, select the **Http Status Code** check box, and then select **Equals** and **404** to change the status when the page is not found. 

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="191" alt="clip_image002[1]" src="http://scug.be/scom/files/2012/06/clip_image002[1_5D005F00_thumb_7F080B9C.jpg" width="244" border="0" />](http://scug.be/scom/files/2012/06/clip_image002[1_5D005F00_5AC3271A.jpg)

5. If you want an alert generated when the health status changes, select the **Generate an alert if any error criteria is met** or **Generate an alert if any warning or error criteria is met** check boxes. 

6. If you want the transaction to stop when an error or warning criteria is met, select the **Stop processing the subsequent requests if any criteria is met** check box. 

7. Click **Verify** to test your changes. 

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="178" alt="image" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_74F36A71.png" width="244" border="0" />](http://scug.be/scom/files/2012/06/image_65A00862.png) 

8. After the changes are verified, click **Apply,** and then close the Web Application Editor. 

Important&#160;&#160; Repeat this process for every monitor that you create. 

&#160;

Next we will [create a distributed appliction](/blogs/scom/archive/2008/10/22/creating-the-distributed-application-models-to-drive-the-service-level-dashboard.aspx) to drive the service level dashboard.

&#160;

Greetz,

Alexandre Verkinderen

[http://scug.be/blogs](/blogs)
