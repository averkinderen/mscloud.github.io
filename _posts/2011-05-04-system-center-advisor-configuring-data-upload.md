---
id: 646
title: System Center Advisor configuring data upload
date: 2011-05-04T11:39:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2011/05/04/system-center-advisor-configuring-data-upload.aspx
permalink: /system-center-advisor-configuring-data-upload/
sc_member_order:
  - "0"
  - "0"
  - "0"
  - "0"
  - "0"
post_views_count:
  - "1857"
  - "1857"
  - "1857"
  - "1857"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Advisor
  - Cloud
  - gateway
  - registry
  - system center
  - system center advisor
---
By default, Advisor will enable the gateway to automatically upload collected data from your server to Advisor. 

To disable automatic data upload, add the following registry entry: 

> Key = HKLMSOFTWAREMicrosoftSystemCenterAdvisorGateway  
> RegEntry name = BlockUpload  
> Entry type = REG_DWORD 

To enable automatic data upload, remove the above registry entry (if present). 

The collected data from agents can be accessed on the gateway machine in the folder located at: <GatewayDataRoot>Mailboxes, where <GatewayDataRoot> is the value of the registry key located at HKLMSOFTWAREMicrosoftSystemCenterAdvisorGateway. The data is stored in a folder specific to each agent, and named after the ID of the agent. This data will be removed from the directory after upload to Advisor by default, or if specified, will be archived for a period of time as specified by in the Archive Period registry key in the same location. The agentID value for a given agent can be found in the following registry entry on the machine running the agent: 

> Key = HKLMSoftwareMicrosoftSystemCenterAdvisor  
> RegEntry name = agentID  
> Entry type = REG_SZ

By default, Advisor will enable the agent to automatically transfer locally collected data to your gateway. 

To disable automatic data upload, add the following registry entry: 

> Key = HKLMSOFTWAREMicrosoftSystemCenterAdvisorAgent  
> RegEntry name = BlockUpload  
> Entry type = REG_DWORD

To enable automatic data upload, remove the above registry entry (if present). 

&#160;

thanks,

Alexandre Verkinderen