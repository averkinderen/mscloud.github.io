---
id: 2921
title: Building a Sharepoint Change Calendar with Orchestrator and Service Manager
date: 2012-11-08T10:48:38+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://scug.be/scom/?p=663
permalink: /building-a-sharepoint-change-calendar-with-orchestrator-and-service-manager-2/
sc_member_order:
  - "0"
post_views_count:
  - "2042"
  - "2042"
  - "2042"
categories:
  - Sharepoint
tags:
  - Service Manager
---
A few weeks ago one of my customers was asking if it’s possible to have a change calendar on the Service Manager portal. Out of the box this is not provided so I asked my good friend Anders how this could be solved. A few days later he already had a nice solution that you can find here: [http://contoso.se/blog/?p=3350&utm\_source=rss&utm\_medium=rss&utm_campaign=building-a-change-calendar-with-orchestrator-and-service-manager](http://contoso.se/blog/?p=3350&utm_source=rss&utm_medium=rss&utm_campaign=building-a-change-calendar-with-orchestrator-and-service-manager "http://contoso.se/blog/?p=3350&utm_source=rss&utm_medium=rss&utm_campaign=building-a-change-calendar-with-orchestrator-and-service-manager") So thank you Anders 🙂

This solution is a perfect viable solution and it works like a charm. So you will be able to create a new change request and see it in your outlook calendar . But when I wanted to start integrating the exchange calendar into SharePoint I encountered some SharePoint limitations.  I couldn’t find an easy and straight forward way to insert the shared exchange calendar into SharePoint.

During my search to integrate my exchange calendar into SharePoint I discovered that you could create SharePoint lists and change the list to a calendar view! So this could be interesting! you can find more info about creating lists and calendar view here: [http://sharepoint.microsoft.com/Blogs/GetThePoint/Lists/Posts/Post.aspx?ID=483](http://sharepoint.microsoft.com/Blogs/GetThePoint/Lists/Posts/Post.aspx?ID=483 "http://sharepoint.microsoft.com/Blogs/GetThePoint/Lists/Posts/Post.aspx?ID=483") . Follow the procedure to create a new SharePoint list and change the view type to a calendar view . Remember the name you will give to your new list as you will need it later on.

Next step is to download the [SharePoint IP](http://orchestrator.codeplex.com/releases/view/75877) and use it to create a new SharePoint list item based on a change request.

Configure the SharePoint Ip:

Note that you need to specify “SharePoint Configuration” and need to provide the name of your list you just created.

[<img style="display: inline; border-width: 0px;" title="image" src="http://www.mscloud.be/wp-content/uploads/2012/11/image_thumb.png" alt="image" width="244" height="170" border="0" />](http://www.mscloud.be/wp-content/uploads/2012/11/image.png)

The runbook monitor Service Manager for new change request, when there is one, the runbook triggers and will create a new list item on Sharepoint

[<img style="display: inline; border-width: 0px;" title="image" src="http://www.mscloud.be/wp-content/uploads/2012/11/image_thumb1.png" alt="image" width="283" height="125" border="0" />](http://www.mscloud.be/wp-content/uploads/2012/11/image1.png)

[<img style="display: inline; border-width: 0px;" title="image" src="http://www.mscloud.be/wp-content/uploads/2012/11/image_thumb2.png" alt="image" width="244" height="170" border="0" />](http://www.mscloud.be/wp-content/uploads/2012/11/image2.png)

[<img style="display: inline; border-width: 0px;" title="image" src="http://www.mscloud.be/wp-content/uploads/2012/11/image_thumb3.png" alt="image" width="244" height="166" border="0" />](http://www.mscloud.be/wp-content/uploads/2012/11/image3.png)

When I create a new change request, Orchestrator will automatically be triggered and put the change request details on the SharePoint List that we have incorporated into our SCSM portal

[<img style="display: inline; border: 0px;" title="image" src="http://www.mscloud.be/wp-content/uploads/2012/11/image_thumb5.png" alt="image" width="341" height="109" border="0" />](http://www.mscloud.be/wp-content/uploads/2012/11/image51.png)

Hope this helps,

Alex