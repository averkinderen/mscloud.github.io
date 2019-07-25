---
id: 9431
title: Azure locations, regions, datacenters, fault domains, update domains, clusters, availability sets??
date: 2015-12-06T12:35:30+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=9431
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
  - "96810"
  - "96810"
  - "96810"
categories:
  - Azure
tags:
  - azure
---
I was at a conference couple of weeks and we were discussing the latest improvements in Azure geo-redundancy across different locations…or was it regions or within different datacenters? But what about fault domains and upgrade domains? This blogpost will review the Azure datacenter model and explain the difference between all of those constructs.

#  Azure Regions

The Azure datacenters are located around the world in strategic places that best meets the customer demands. These areas are known as Azure regions and are placed at a distance of at least 300miles or 480km from each other in case there is a natural disaster that would affect more than one region at a time.

Azure operates out of 20 regions around the world at the time of writing this blog post. Geographic expansion is a priority for Azure because it enables the customers to achieve higher performance and it supports their requirements and preferences regarding data location.

[<img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border: 0px;" title="image" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/12/image_thumb.png" alt="image" width="244" height="136" border="0" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/12/image.png)

In the table below you can find the Azure regions and location. For the latest list of Azure datacenter locations, see [Azure Regions](http://azure.microsoft.com/regions/). <u></u>

<table style="border-collapse: collapse; border-bottom-style: none; line-height: normal;" border="0" width="260" cellspacing="0" cellpadding="0">
  <colgroup> <col style="width: 74pt; mso-width-source: userset; mso-width-alt: 3527;" width="99" /> <col style="width: 82pt; mso-width-source: userset; mso-width-alt: 3896;" width="110" /></colgroup> <tr style="height: 19.2pt;">
    <td class="xl65" style="border-right: windowtext 0.5pt solid; border-top-color: windowtext; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; border-top-width: 0.5pt; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="32">
      <div data-tab-panel-id="regions">
        <span style="font-family: 'Segoe UI';"><span style="font-size: 7pt; color: #505050;"><strong>Azure Region</strong></span></span>
      </div>
    </td>
    
    <td class="xl65" style="border-right: windowtext 0.5pt solid; border-top-color: windowtext; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; border-top-width: 0.5pt; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 7pt; color: #505050;"><strong>Location</strong></span></span>
    </td>
  </tr>
  
  <tr style="height: 14.4pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="23">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Central US</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Iowa</span></span>
    </td>
  </tr>
  
  <tr style="height: 14.4pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="23">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">East US</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Virginia</span></span>
    </td>
  </tr>
  
  <tr style="height: 14.4pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="23">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">East US 2</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Virginia</span></span>
    </td>
  </tr>
  
  <tr style="height: 22.8pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="37">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">US Gov Iowa</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Iowa</span></span>
    </td>
  </tr>
  
  <tr style="height: 22.8pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="37">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">US Gov Virginia</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Virginia</span></span>
    </td>
  </tr>
  
  <tr style="height: 22.8pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="37">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">North Central US</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Illinois</span></span>
    </td>
  </tr>
  
  <tr style="height: 22.8pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="37">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">South Central US</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Texas</span></span>
    </td>
  </tr>
  
  <tr style="height: 14.4pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="23">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">West US</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">California</span></span>
    </td>
  </tr>
  
  <tr style="height: 22.8pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="37">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">North Europe</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Ireland</span></span>
    </td>
  </tr>
  
  <tr style="height: 22.8pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="37">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">West Europe</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Netherlands</span></span>
    </td>
  </tr>
  
  <tr style="height: 14.4pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="23">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">East Asia</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Hong Kong</span></span>
    </td>
  </tr>
  
  <tr style="height: 22.8pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="37">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Southeast Asia</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Singapore</span></span>
    </td>
  </tr>
  
  <tr style="height: 22.8pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="37">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Japan East</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Tokyo, Saitama</span></span>
    </td>
  </tr>
  
  <tr style="height: 14.4pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="23">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Japan West</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Osaka</span></span>
    </td>
  </tr>
  
  <tr style="height: 22.8pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="37">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Brazil South</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Sao Paulo State</span></span>
    </td>
  </tr>
  
  <tr style="height: 22.8pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="37">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Australia East</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">New South Wales</span></span>
    </td>
  </tr>
  
  <tr style="height: 22.8pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="37">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Australia Southeast</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Victoria</span></span>
    </td>
  </tr>
  
  <tr style="height: 14.4pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="23">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Central India</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Pune</span></span>
    </td>
  </tr>
  
  <tr style="height: 14.4pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="23">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">South India</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Chennai</span></span>
    </td>
  </tr>
  
  <tr style="height: 14.4pt;">
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: windowtext 0.5pt solid; background-color: white; padding: 1px 1px 0px 1px;" width="123" height="23">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">West India</span></span>
    </td>
    
    <td class="xl66" style="border-top: medium none; border-right: windowtext 0.5pt solid; vertical-align: top; border-bottom: windowtext 0.5pt solid; border-left: medium none; background-color: white; padding: 1px 1px 0px 1px;" width="136">
      <span style="font-family: 'Segoe UI';"><span style="font-size: 8pt; color: #505050;">Mumbai</span></span></p> 
      
      <div>
      </div>
      
      <div>
      </div>
    </td>
  </tr>
</table>

Before you can deploy anything in Azure you need to have an understanding of the following:

  * What is a Region?
  * Where are the regions located?
  * What are the different capabilities of the regions with respect to each other?
  * What are the preview features vs. general availability within a region?
  * Are there any restrictions on where you can deploy to a region? For example: Legal compliance, Government regulations?

It is very important to correctly choose a region or regions that meet your organization’s needs. There are a number of elements to consider when choosing a region to deploy your applications and services:

  * Data
  * Location of service consumers
  * Service capability and availability
  * Network performance
  * Pricing
  * Redundancy for high availability

### Data

Where the data is physically stored is very important for customers. When a storage account is created, the customer chooses the primary location for their storage account. However, the secondary location for the storage account is fixed and customers do not have the ability to change this. The following table shows the current primary and secondary location pairings:

<table class="PlainTable11" style="border-collapse: collapse; text-align: left; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-yfti-tbllook: 1056; mso-padding-alt: 0in 5.4pt 0in 5.4pt;" border="1" width="389" cellspacing="0" cellpadding="0">
  <tr style="mso-yfti-irow: -1; mso-yfti-firstrow: yes; mso-yfti-lastfirstrow: yes;">
    <td style="background: gray; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 128; border: #bfbfbf 1pt solid; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p class="MsoNormal" style="margin: 6pt 0in; line-height: normal; mso-yfti-cnfc: 1;">
        <b style="mso-bidi-font-weight: normal;"><span lang="EN-AU" style="mso-fareast-font-family: calibri; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #ffffff; font-size: xx-small;">Primary Region</span></span></span></b><b style="mso-bidi-font-weight: normal;"></b>
      </p>
    </td>
    
    <td style="border-top: #bfbfbf 1pt solid; border-right: #bfbfbf 1pt solid; background: gray; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 128; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p class="MsoNormal" style="margin: 6pt 0in; line-height: normal; mso-yfti-cnfc: 1;">
        <b style="mso-bidi-font-weight: normal;"><span lang="EN-AU" style="mso-fareast-font-family: calibri; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #ffffff; font-size: xx-small;">Secondary Region</span></span></span></b>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 0;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">North Central US</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">South Central US</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 1;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">South Central US</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">North Central US</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 2;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">East US</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">West US</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 3;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">West US</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">East US</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 4;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">US East 2</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">Central US</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 5;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">Central US</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">US East 2</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 6;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">North Europe</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">West Europe</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 7;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">West Europe</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">North Europe</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 8;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">Southeast Asia</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">East Asia</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 9;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">East Asia</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">Southeast Asia</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 10;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">East China</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">North China</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 11;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">North China</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">East China</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 12;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">Japan East</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">Japan West</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 13;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">Japan West</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">Japan East</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 14;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">Brazil South</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">South Central US</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 15;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">Australia East</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">Australia Southeast</span></span></span>
      </p>
    </td>
  </tr>
  
  <tr style="mso-yfti-irow: 16; mso-yfti-lastrow: yes;">
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: #bfbfbf 1pt solid; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="202">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-bidi-font-weight: bold; mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">Australia Southeast</span></span></span>
      </p>
    </td>
    
    <td style="border-top: medium none; border-right: #bfbfbf 1pt solid; background: #f2f2f2; border-bottom: #bfbfbf 1pt solid; border-left: medium none; mso-border-alt: solid #bfbfbf .5pt; mso-border-themecolor: background1; mso-border-themeshade: 191; mso-background-themecolor: background1; mso-background-themeshade: 242; mso-border-left-alt: solid #bfbfbf .5pt; mso-border-left-themecolor: background1; mso-border-left-themeshade: 191; mso-border-top-alt: solid #bfbfbf .5pt; mso-border-top-themecolor: background1; mso-border-top-themeshade: 191; mso-border-bottom-themecolor: background1; mso-border-bottom-themeshade: 191; mso-border-right-themecolor: background1; mso-border-right-themeshade: 191; padding: 0in 5.4pt 0in 5.4pt;" valign="top" width="187">
      <p style="margin: 6pt 0in 0pt; mso-yfti-cnfc: 64;">
        <span lang="EN-AU" style="mso-ansi-language: en-au; mso-fareast-language: en-au;"><span style="font-family: 'Segoe UI';"><span style="color: #000000; font-size: xx-small;">Australia East</span></span></span>
      </p>
    </td>
  </tr>
</table>

### Service capability and availability

Not all Azure services are available everywhere at the same time. Azure will first release a new feature in preview to only a subset of regions, prior to being generally available.

Before deploying an Azure service, review the following link and choose a region or regions to verify what services are available in your selected region: [Services by region](http://azure.microsoft.com/en-us/regions/#services).

### Network performance

It is best to validate the latency between the customer location and Microsoft Azure regions. Choose the one with the lowest latency, which will provide the best performance from a networking perspective. You can test the network latency with this tool for examaple: [http://www.azurespeed.com/](http://www.azurespeed.com/ "http://www.azurespeed.com/")

[<img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border: 0px;" title="image" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/12/image_thumb1.png" alt="image" width="644" height="357" border="0" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/12/image1.png)

## Pricing

The pricing can be different for different regions for the same services. The cost for Azure Services is controlled by many factors. If latency is not important for your application you may deploy it in a region with a lower cost. In some regions however are only for a certain set of customers. The Australian region is only for customers with a business pressense in Australia or New Zealand. Please refer to the following site for the pricing details of each service provided by Microsoft Azure: [Azure Pricing](http://azure.microsoft.com/en-us/pricing/).

## Datacenter Architecture

As described earlier, Azure hosts its services in a series of globally distributed datacenters. These datacenters are located in a specific location and are grouped together in regions. Datacenters within a given region are divided into “clusters,” which host the Azure services.  Within each datacenter, the racks of equipment are built to be fault tolerant on a networking, physical host servers, storage, and power level. The physical host servers are placed in high availability units called a cluster.

[<img style="background-image: none; padding-top: 0px; padding-left: 0px; display: inline; padding-right: 0px; border: 0px;" title="image" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/12/image_thumb2.png" alt="image" width="644" height="233" border="0" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/12/image2.png)

One single rack is referred to as a Fault Domain (FD), and it can be viewed as a vertical partitioning of the hardware. A second partition within the datacenter is called the Upgrade Domain (UD) and it can be viewed as a set of horizontal stripes passing through the vertical racks of fault domains. To provide redundancy to your application, we recommend that you group two or more virtual machines in an Availability Set. This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available. Each virtual machine in your Availability Set is assigned an Update Domain (UD) and a Fault Domain (FD) by the underlying Azure platform. The following diagram shows a high-level relationship between fault domains and update domains in the Azure datacenters.

<img src="https://acomdpsstorage.blob.core.windows.net/dpsmedia-prod/azure.microsoft.com/en-us/documentation/articles/virtual-machines-manage-availability/20151022044944/ud-fd-configuration.png" alt="UD FD configuration" width="640" height="420" /> 

Virtual machines are placed in specific fault domains and update domains based on the location of respective virtual machines in the same Availability Set.

### Fault Domains

The fault domain is considered the lowest common denominator within the datacenter for fault tolerance. Microsoft Azure can lose a complete rack, and the hosted services can continue unaffected. FDs define the group of virtual machines that share a common power source and network switch. By default, the virtual machines configured within your Availability Set are separated across two FDs. While placing your virtual machines into an Availability Set does not protect your application from operating system or application-specific failures, it does limit the impact of potential physical hardware failures, network outages, or power interruptions.

### Upgrade domains

Upgrade domains are used to deploy updates (security patches) within Azure without affecting the availability of the running services within the Azure fabric. For a given Availability Set, five non-user-configurable UDs are assigned to indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time. When more than five virtual machines are configured within a single Availability Set, the sixth virtual machine will be placed into the same UD as the first virtual machine, the seventh in the same UD as the second virtual machine, and so on. The order of UDs being rebooted may not proceed sequentially during planned maintenance, but only one UD will be rebooted at a time.

# Conclusion

I hope you have a understanding now of the differences between Azure regions, locations and so on and how the different Azure architectural constructs relate to each other.

Kind regards,

Alexandre Verkinderen
