---
id: 1711
title: enable audit collection on opsmgr agents
date: 2008-08-28T14:44:59+10:00
author: alexandre@verkinderen.com

guid: /blogs/scom/archive/2008/08/28/enable-audit-collection-on-opsmgr-agents.aspx
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1409"
  - "1409"
  - "1409"
  - "1409"
  - "1409"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Uncategorized
---
Depending on your auditing needs, you might have several hundred to thousands of computers from which you want to collect audit events. By default, the service needed for an agent to be an Audit Collection Services (ACS) forwarder is installed but not enabled when the Operations Manager agent is installed. After you install the ACS collector and database you can then remotely enable this service on multiple agents through the Operations Manager console by running the **Enable Audit Collection** task.

This procedure should be run after the ACS collector and database are installed and can only be run against computers that already have the Operations Manager agent installed. In addition, the user account that runs this task must belong to the local Administrators group on each agent computer.

#### To enable audit collection on Operations Manager 2007 agents

1. Log on to the computer with an account that is a member of the Operations Manager Administrators role for your Operations Manager 2007 Management Group. This account must also have the rights of a local administrator on each agent computer that you want to enable as an ACS forwarder.

2. In the Operations Console, click the **Monitoring** button.

******Note** 

When you run the Operations Console on a computer that is not a Management Server, the **Connect To Server** dialog box displays. In the **Server name** text box, type the name of the Operations Manager 2007 Management Server that you want the Operations Console to connect to.

3. In the Monitoring pane, expand **Operations Manager**, expand **Agent**, and then click **Agent Health State**. This view has two panes, and the actions in this procedure are performed in the right pane.

&nbsp;

4. In the details pane, click all agents that you want to enable as ACS forwarders. You can make multiple selections by pressing CTRL or SHIFT.

5. In the **Actions** pane, under **Health Service Tasks**, click **Enable Audit Collection**. The **Run Task &#8211; Enable Audit Collection** dialog box displays.

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="244" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/enableauditcollectiononopsmgragents_E9C2/image_thumb_4.png" width="201" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/enableauditcollectiononopsmgragents_E9C2/image_10.png)

6. In the **Task Parameters** section, click **Override**. The **Override Task Parameters** dialog box displays.

7. In the **Override the task parameters with the new values** section, click the _CollectorServer_ parameter; in the **New Value** column, type the FQDN of the ACS collector; and then click **Override**.

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="190" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/enableauditcollectiononopsmgragents_E9C2/image_thumb_6.png" width="244" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/enableauditcollectiononopsmgragents_E9C2/image_14.png)

8. In the **Task credentials** section, click **Other**. In the **User Name** box, type the name of a user account that belongs to the local Administrators group on the agent computers. In the **Password** box, type the password for this user account. Click to expand the **Domain** drop-down list to view the available domains, and then click the domain of the user account.

9. Click **Run Task**. The **Task Status** dialog box displays tracking the progress of the task.

[<img style="border-right: 0px;border-top: 0px;border-left: 0px;border-bottom: 0px" height="244" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/enableauditcollectiononopsmgragents_E9C2/image_thumb_7.png" width="200" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/enableauditcollectiononopsmgragents_E9C2/image_16.png)

10. When the task completes successfully, click **Close**

Watch for this event on your forwarder:

[<img style="border-top-width: 0px;border-left-width: 0px;border-bottom-width: 0px;border-right-width: 0px" height="244" alt="image" src="http://scug.be/blogs/scom/WindowsLiveWriter/enableauditcollectiononopsmgragents_E9C2/image_thumb_5.png" width="221" border="0" />](http://scug.be/blogs/scom/WindowsLiveWriter/enableauditcollectiononopsmgragents_E9C2/image_12.png)

&nbsp;

Wait a few minutes and your ready to collect your auditing events!

&nbsp;

Greetz,

Alexandre verkinderen

<http://scug.be/blogs/scom>

&nbsp;

<div class="wlWriterSmartContent" style="padding-right: 0px;padding-left: 0px;padding-bottom: 0px;margin: 0px;padding-top: 0px">
  Tags van Technorati: <a href="http://technorati.com/tags/acs" rel="tag">acs</a>,<a href="http://technorati.com/tags/audit%20collection%20service" rel="tag">audit collection service</a>,<a href="http://technorati.com/tags/opmsgr" rel="tag">opmsgr</a>,<a href="http://technorati.com/tags/scom" rel="tag">scom</a>
</div>
