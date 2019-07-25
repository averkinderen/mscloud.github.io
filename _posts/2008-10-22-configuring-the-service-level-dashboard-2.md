---
id: 1761
title: Configuring the Service Level Dashboard Part V
date: 2008-10-22T21:08:00+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2008/10/22/configuring-the-service-level-dashboard.aspx
permalink: /configuring-the-service-level-dashboard-2/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "2693"
  - "2693"
  - "2693"
  - "2693"
  - "2693"
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
After you create your monitors and distributed applications, you must take some additional steps to configure the Service Level Dashboard group and service level goal properties. Discovery finds all the objects that are associated with a distributed application. The current setting of these attributes is displayed in the Service Level Dashboard Attributes view in the Operations Console. This view lists the distributed applications that can be shown on the Service Level Dashboard, their Dashboard group, and their current service level goals.

&nbsp;

<table class="MsoNormalTable" style="border-right: medium none;border-top: medium none;margin-left: 5.4pt;border-left: medium none;border-bottom: medium none;border-collapse: collapse" border="1" cellpadding="0" cellspacing="0">
  <tr>
    <td style="border: 1pt solid windowtext;padding: 0cm 5.4pt;background: #d9d9d9 none repeat scroll 0% 0%;width: 76.5pt" valign="top" width="102">
      <p class="MsoNormal">
        <span lang="EN-US">Property </span>
      </p>
    </td>
    
    <td style="padding: 0cm 5.4pt;background: #d9d9d9 none repeat scroll 0% 0%;width: 49.5pt" valign="top" width="66">
      <p class="MsoNormal">
        <span lang="EN-US">Default </span>
      </p>
    </td>
    
    <td style="padding: 0cm 5.4pt;background: #d9d9d9 none repeat scroll 0% 0%;width: 311.4pt" valign="top" width="415">
      <p class="MsoNormal">
        <span lang="EN-US">Description</span>
      </p>
    </td>
  </tr>
  
  <tr>
    <td style="padding: 0cm 5.4pt;width: 76.5pt" valign="top" width="102">
      <p class="MsoNormal">
        <span lang="EN-US">Name</span>
      </p>
    </td>
    
    <td style="padding: 0cm 5.4pt;width: 49.5pt" valign="top" width="66">
      <p class="MsoNormal">
        <span lang="EN-US">&nbsp;</span>
      </p>
    </td>
    
    <td style="padding: 0cm 5.4pt;width: 311.4pt" valign="top" width="415">
      <p class="MsoNormal">
        <span lang="EN-US">The distributed application name</span>
      </p>
    </td>
  </tr>
  
  <tr>
    <td style="padding: 0cm 5.4pt;width: 76.5pt" valign="top" width="102">
      <p class="MsoNormal">
        <span lang="EN-US">Availability Service Level Threshold</span>
      </p>
    </td>
    
    <td style="padding: 0cm 5.4pt;width: 49.5pt" valign="top" width="66">
      <p class="MsoNormal">
        <span lang="EN-US">95</span>
      </p>
    </td>
    
    <td style="padding: 0cm 5.4pt;width: 311.4pt" valign="top" width="415">
      <p class="MsoNormal">
        <span lang="EN-US">The percentage of availability the application must achieve to be shown as in compliance with the availability service level</span>
      </p>
    </td>
  </tr>
  
  <tr>
    <td style="padding: 0cm 5.4pt;width: 76.5pt" valign="top" width="102">
      <p class="MsoNormal">
        <span lang="EN-US">Performance Service Level Threshold</span>
      </p>
    </td>
    
    <td style="padding: 0cm 5.4pt;width: 49.5pt" valign="top" width="66">
      <p class="MsoNormal">
        <span lang="EN-US">95</span>
      </p>
    </td>
    
    <td style="padding: 0cm 5.4pt;width: 311.4pt" valign="top" width="415">
      <p class="MsoNormal">
        <span lang="EN-US">The percentage of performance the application must achieve to be shown as in compliance with the performance service level</span>
      </p>
    </td>
  </tr>
  
  <tr>
    <td style="padding: 0cm 5.4pt;width: 76.5pt" valign="top" width="102">
      <p class="MsoNormal">
        <span lang="EN-US">Dashboard Group</span>
      </p>
    </td>
    
    <td style="padding: 0cm 5.4pt;width: 49.5pt" valign="top" width="66">
      <p class="MsoNormal">
        <span lang="EN-US">1</span>
      </p>
    </td>
    
    <td style="padding: 0cm 5.4pt;width: 311.4pt" valign="top" width="415">
      <p class="MsoNormal">
        <span lang="EN-US">The Dashboard Group setting controls which dashboard the model will display on. All applications are assigned a default setting of 1, which allows multiple dashboards to be created for multiple views of the applications, or for views of different applications.</span>
      </p>
    </td>
  </tr>
  
  <tr>
    <td style="padding: 0cm 5.4pt;width: 76.5pt" valign="top" width="102">
      <p class="MsoNormal">
        <span lang="EN-US">GUID</span>
      </p>
    </td>
    
    <td style="padding: 0cm 5.4pt;width: 49.5pt" valign="top" width="66">
      <p class="MsoNormal">
        <span lang="EN-US">&nbsp;</span>
      </p>
    </td>
    
    <td style="padding: 0cm 5.4pt;width: 311.4pt" valign="top" width="415">
      <p class="MsoNormal">
        <span lang="EN-US">The GUID of the distributed application</span>
      </p>
    </td>
  </tr>
</table>

&nbsp;

#### <a name="_Toc206825607">Change the Service Level Dashboard Attributes for an Application</a>

To change the Service Level Dashboard attributes, use overrides.

**To override Service Level Dashboard attributes for a distributed application**

  1. Open the Authoring pane.</p> 
  2. Expand **Management Pack Objects**, and then click **Object Discoveries**.

  3. In the **Look for** box, type **SLDBase** and then click **Find Now**.

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" alt="clip_image002[1]" src="http://scug.be/scom/files/2012/06/clip_image002[1_5D005F00_thumb_5018F38C.jpg" width="244" border="0" height="210" />](http://scug.be/scom/files/2012/06/clip_image002[1_5D005F00_37F58931.jpg)

  1. Click **Enterprise Service Monitoring Service Level Dashboard Discovery** and then, in the **Actions** pane, click **Overrides**. 

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" alt="clip_image002[3]" src="http://scug.be/scom/files/2012/06/clip_image002[3_5D005F00_thumb_1F363C21.jpg" width="244" border="0" height="178" />](http://scug.be/scom/files/2012/06/clip_image002[3_5D005F00_41DA7A9C.jpg)

  1. Click **Override the Object Discovery** and then click **For a specific object of type: Service Level Dashboard Application**.</p> 
  2. In the **Select Object** box, select the distributed application that contains attributes you want to edit, and then click **OK**.

  3. Select the **Override** check box next to the attribute you want to edit.

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" alt="clip_image002[5]" src="http://scug.be/scom/files/2012/06/clip_image002[5_5D005F00_thumb_04F5D2FD.jpg" width="239" border="0" height="244" />](http://scug.be/scom/files/2012/06/clip_image002[5_5D005F00_6CD268A1.jpg)

  1. Enter the adjusted setting in the **Override Setting** column. 

a. For **Dashboard Group**, enter an integer or a string.

b. For the **Performance and Availability Service Level Thresholds**, enter the uptime percentage in a decimal number, without any symbols.

  1. Click **OK**. 

&nbsp;

Now that everything is configured we can start using our [service level dashboard](/blogs/scom/archive/2008/10/22/service-level-dashboard-part-vi.aspx)!

****&nbsp;

**Greetz,**

**ALexandre Verkinderen**
