---
id: 1741
title: Creating the Distributed Application Models to Drive the Service Level Dashboard Part IV
date: 2008-10-22T21:06:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2008/10/22/creating-the-distributed-application-models-to-drive-the-service-level-dashboard.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "3046"
  - "3046"
  - "3046"
  - "3046"
  - "3046"
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
The distributed application model interface provides a flexible way to customize the Service Level Dashboard display to your needs. The Service Level Dashboard accepts a simple distributed application model as its configuration for application listings and transaction groupings. This model allows you to group Web applications or other monitors on the Service Level Dashboard into applications and regions. You can define how the health rolls up to the component group and the application as a whole by editing the health rollup of the distributed application model. 

Important&#160;&#160; Note that these distributed application models are in addition to any distributed application models you might have already created for your applications. The Service Level Dashboard works only with a specific style of distributed application model—one that is based on the Service Level Dashboard Application template. 

The Service Level Dashboard display shows three levels. The top level lists applications by their distributed application model names, the second level shows the component groups, and the third level lists the actual transaction names. Each level can contain several entries. 

&#160;

**To create a distributed application model** 

1. In the Operations Console, click **Authoring**, right-click **Distributed Applications**, and then click **Create a new distributed application**. 

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="220" alt="clip_image002[1]" src="http://scug.be/scom/files/2012/06/clip_image002[1_5D005F00_thumb_27C28510.jpg" width="244" border="0" />](http://scug.be/scom/files/2012/06/clip_image002[1_5D005F00_1DDD93A5.jpg)

2. In the **Name** box, type a name for the distributed application, which will appear on the Service Level Dashboard. In the **Description** box, you can type a description. 

3. Under **Template**, select the **Service Level Dashboard Application** template. 

4. In the **Management Pack** drop-down box, choose the management pack created in the previous steps from the list of unsealed management packs. (By default, the distributed application you create is saved to the Default Management Pack.) Or, click **New** to create a new management pack. Click **OK**. 

**To design your distributed application model** 

1. The diagram pane in the distributed application designer displays the component groups of your distributed application. You will see two component groups defined by the template: Component Group 1 and Component Group 2. Right-click each component group to review it. If necessary, edit the object types that are included in your distributed application, and modify the name. On the toolbar, click **Add Component** to create a new component group. Component groups are generally used to define regions or other groups of transactions on the report. 

2. The buttons at the bottom of the **Objects** pane list all object types that are defined by the template you chose earlier. If your distributed application does not contain one or more of the components shown in the list, click **Organize Object Types** to view a list of all currently included object types. Clear the check box for any object type that is not part of your distributed application. 

3. Click each of the remaining buttons at the bottom of the **Objects** pane to view the objects that are listed in each. By default, the list contains all the discovered objects on your network that are of that object type. 

4. Right-click each object that is a component of your distributed application, point to **Add To**, and then click the name of the component group to which this object belongs. (These objects may be the Web monitors defined earlier, or other types of objects that you want to display on the Service Level Dashboard at the transaction level. Any item in the component group displays as a transaction, with its health state calculated.) Click **Save**. 

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="179" alt="clip_image002[3]" src="http://scug.be/scom/files/2012/06/clip_image002[3_5D005F00_thumb_7F43A2FB.jpg" width="244" border="0" />](http://scug.be/scom/files/2012/06/clip_image002[3_5D005F00_3C47D48E.jpg)

5. To configure the health rollup of the distributed application (and by extension the Service Level Dashboard), in the **Component Group Details** pane, click the **Configure health rollup** link, and create an override for the rollup algorithm for the component group (or entire model) that rolls up in the manner expected. 

6. To save the distributed application to a management pack, click **Save**. 

&#160;

After you create your monitors and distributed applications, you must take some [additional steps to configure](/blogs/scom/archive/2008/10/22/configuring-the-service-level-dashboard.aspx) the Service Level Dashboard group and service level goal properties. 

Greetz, 

Alexandre Verkinderen 

[http://scug.be/blogs](/blogs)
