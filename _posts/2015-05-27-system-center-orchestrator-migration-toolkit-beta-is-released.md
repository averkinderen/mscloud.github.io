---
id: 9001
title: 'System Center Orchestrator Migration Toolkit’- Beta is released'
date: 2015-05-27T09:32:09+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=9001
sc_member_order:
  - "0"
bpxl_standard_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_standard_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_image_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_image_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_audio_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_audio_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_video_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_video_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_link_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_link_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_gallery_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_gallery_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_status_excerpt_home:
  - "0"
  - "0"
  - "0"
bpxl_status_single_hide:
  - "0"
  - "0"
  - "0"
bpxl_singlerelated:
  - "0"
  - "0"
  - "0"
post_views_count:
  - "3467"
  - "3467"
  - "3467"
categories:
  - SystemCenter
tags:
  - automation
  - Azure
  - scorch
  - WAP
---
<p class="x_MsoNormal">
  <b><u>What is System Center Orchestrator Migration Toolkit</u></b>
</p>

<p class="x_MsoNormal">
  This toolkit will contain collection of tools for migrating integration packs, standard activities, and runbooks from System Center 2012 – Orchestrator to Azure Automation and Service Management Automation.  Included in this <b>beta</b> release are
</p>

<p class="x_MsoListParagraph">
  ·        <b>Integration Pack converter</b>
</p>

<p class="x_MsoListParagraph">
  ·        <b>Standard Activity Module</b>
</p>

<p class="x_MsoListParagraph">
  ·        <b><span lang="EN">System Center Orchestrator Integration Modules </span></b>(converted modules for Microsoft released and supported OIT based IPs &#8211; separate download).
</p>

<p class="x_MsoNormal">
  <p class="x_MsoNormal">
    <b><u>System Center Orchestrator Migration Toolkit- Details</u></b>
  </p>
  
  <p class="x_MsoNormal">
    <p class="x_MsoNormal">
      <b>Integration Pack Converter</b>
    </p>
    
    <p class="x_MsoNormal">
      The Integration Pack Converter converts integration packs that were created using the Orchestrator Integration Toolkit (OIT) to integration modules based on Windows PowerShell that can be imported into Azure Automation or Service Management Automation.
    </p>
    
    <p class="x_MsoNormal">
      When you run the Integration Pack Converter, you are presented with a wizard that will allow you to select an integration pack (.oip) file. The wizard then lists the activities included in that integration pack and allows you to select which will be migrated and allows for all activity modifications/validations. When you complete the wizard, it creates a module that includes a corresponding cmdlet for each of the activities in the original integration pack.
    </p>
    
    <p class="x_MsoNormal">
      <p class="x_MsoNormal">
        <b>Standard Activities Module</b>
      </p>
      
      <p class="x_MsoNormal">
        Orchestrator includes a set of out-of-box standard activities that are not included in an integration pack but are used by many runbooks. The Standard Activities module is a integration module that includes a cmdlet equivalent for each of these activities. In addition to supporting converted runbooks, the cmdlets in the standard activities module can be used by someone familiar with Orchestrator to build new runbooks in SMA/Azure Automation.
      </p>
      
      <p class="x_MsoNormal">
        <p class="x_MsoNormal">
          <b>Download link: </b>Migration Toolkit: <a href="http://www.microsoft.com/en-us/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all" target="_blank">http://www.microsoft.com/en-us/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all</a><b></b>
        </p>
        
        <p class="x_MsoNormal">
          <p class="x_MsoNormal">
            <b><span lang="EN">System Center Orchestrator Integration Modules</span>:</b>
          </p>
          
          <p class="x_MsoNormal">
            For customers convenience, we converted the Microsoft supported and released Orchestrator Integration toolkit (OIT) based IPs, and are shipping integration modules so that they can be directly imported into Service Management Automation/Azure Automation.
          </p>
          
          <p class="x_MsoNormal">
            <p class="x_MsoNormal">
              <b>Download link:</b> <a href="http://www.microsoft.com/en-us/download/details.aspx?id=47324" target="_blank">http://www.microsoft.com/en-us/download/details.aspx?id=47324</a>
            </p>
