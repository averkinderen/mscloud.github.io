---
id: 11061
title: Power BI for SCSM
date: 2016-09-09T02:17:09+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=11061
sc_member_order:
  - "0"
  - "0"
  - "0"
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
  - "6449"
  - "6449"
  - "6449"
image: /wp-content/uploads/2016/09/image_thumb8-150x142.png
categories:
  - Azure
  - SystemCenter
tags:
  - Azure
  - cubesys
  - Power BI
  - SCSM
  - Service Manager
  - system center
---
As part of delivering our managed services at <a href="http://cubesys.com.au" target="_blank">cubesys</a> we are using System Center Service Manager for incident logging and request management. We wanted to enhance the customer experience by providing visually stunning reports and dashboards so we started to investigate at how we could leverage Microsoft Power BI together with Service Manager SQL Analysis. There are a few advantages to using the Service Manager SQL SSAS multidimensional objects vs the traditional Service Manager database such as:

  * Cubes
  * Perspectives
  * Measure Groups
  * Measures
  * Dimensions
  * Dimension Attributes
  * Hierarchies including Parent Child

#  Getting Started

This blog post is going to cover the requirements needed to connect Power BI to your SCSM environment and will document the steps to create you own Power BI dashboard:

  * First make sure you have a Power BI Pro account. If not you can easily create one at <http://app.powerbi.com>
  * You will also need a Power BI Enterprise Gateway to connect from Power BI Online to your SQL Analysis Server
  * Next download the Power BI desktop app and sign in with you Power BI account. (Make sure you always have the latest version of Power BI desktop as the product team is regularly improving and updating Power BI)

Once Power BI desktop is open click on **Get data** and select **SQL Server Analyses Services Database.** You will have to provide your server name and credentials

[<img class="size-medium wp-image-10861 alignnone" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image-274x300.png" alt="image.png" width="274" height="300" srcset="/wp-content/uploads/2016/09/image-274x300.png 274w, /wp-content/uploads/2016/09/image.png 701w" sizes="(max-width: 274px) 100vw, 274px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image.png)

As you can see in the screenshot below I was unable to connect Live to my SQL Analysis Server. I could only use the import functionality which means I need to select, one-by-one the different tables I want to import and, most importantly, define the relationships.  Which is really a tedious job….

[<img class="alignnone size-medium wp-image-10881" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image1-300x142.png" alt="image1.png" width="300" height="142" srcset="/wp-content/uploads/2016/09/image1-300x142.png 300w, /wp-content/uploads/2016/09/image1-768x362.png 768w, /wp-content/uploads/2016/09/image1.png 1024w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image1.png)

&nbsp;

Apparently you can only use the “Connect Live” capability if you are running SQL Enterprise and not if you are using SQL Standard. Power BI issues DAX queries against SSAS and this is not supported in Standard (until SQL Server 2016). So if you hit this issue and need “Connect Live” please upgrade your SQL to Enterprise.

## Limitations of Analysis Services live connections

You can use a live connection against tabular or multidimensional instances.

<table border="1" cellspacing="0" cellpadding="0">
  <tr>
    <td valign="top">
      <b>Server version</b>
    </td>
    
    <td valign="top">
      <b>Required SKU</b>
    </td>
  </tr>
  
  <tr>
    <td valign="top">
      2012 SP1 CU4 or later
    </td>
    
    <td valign="top">
      Business Intelligence and Enterprise SKU
    </td>
  </tr>
  
  <tr>
    <td valign="top">
      2014
    </td>
    
    <td valign="top">
      Business Intelligence and Enterprise SKU
    </td>
  </tr>
  
  <tr>
    <td valign="top">
      2016
    </td>
    
    <td valign="top">
      Standard SKU or higher
    </td>
  </tr>
</table>

  * Cell level Formatting and translation features are not supported.
  * Actions and Named Sets are not exposed to Power BI, but you can still connect to multidimensional cubes that also contain Actions or Named sets and create visuals and reports

Once you have upgraded to SQL Enterprise you will be able to Connect Live as seen in the picture below:

[<img class="alignnone size-medium wp-image-10901" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image2-300x146.png" alt="image2.png" width="300" height="146" srcset="/wp-content/uploads/2016/09/image2-300x146.png 300w, /wp-content/uploads/2016/09/image2-768x374.png 768w, /wp-content/uploads/2016/09/image2.png 1024w, /wp-content/uploads/2016/09/image2-330x160.png 330w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image2.png)

Select the following cubes to import Incident related information

[<img class="alignnone size-medium wp-image-10921" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image3-300x238.png" alt="image3.png" width="300" height="238" srcset="/wp-content/uploads/2016/09/image3-300x238.png 300w, /wp-content/uploads/2016/09/image3-768x609.png 768w, /wp-content/uploads/2016/09/image3.png 968w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image3.png)

# Build your dashboard

On the right hand side of your Power Bi desktop app you will see the dataset and the different dimensions and measures:

[<img class="alignnone size-medium wp-image-10932" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image4-230x300.png" alt="image4.png" width="230" height="300" srcset="/wp-content/uploads/2016/09/image4-230x300.png 230w, /wp-content/uploads/2016/09/image4.png 590w" sizes="(max-width: 230px) 100vw, 230px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image4.png)

You will see different types of data in your dataset:

### Measures, measure groups and KPIs

Measure groups in a multidimensional cube are exposed in Power BI as tables with the ∑ sign beside them in the **Fields** pane. Calculated measures that don&#8217;t have an associated measure group are grouped under a special table called _Measures_ in the tabular metadata.

### Parent-child hierarchies

Multidimensional models support Parent-child hierarchies, which are presented as a _hierarchy_ in the tabular metadata. Each level of the Parent-child hierarchy is exposed as a hidden column in the tabular metadata. The key attribute of the Parent-child dimension is not exposed in the tabular metadata.

## Custom Power BI visuals

To be able to use the “date” and “calendar” fields in Power BI I had to import a custom Power BI visual. Please have a look here for the all the custom visuals that are available [https://app.powerbi.com/visuals/](https://app.powerbi.com/visuals/ "https://app.powerbi.com/visuals/") . Make sure you download the following custom visuals as you will need them in this report:

  * Timeline
  * Donut Chart
  * Circular Gauge

## Design your Report

**Click** on the **Timeline** visual to add it to the report and add the field labelled **Calendardate**

[<img class="alignnone size-medium wp-image-10951" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image5-300x121.png" alt="image5.png" width="300" height="121" srcset="/wp-content/uploads/2016/09/image5-300x121.png 300w, /wp-content/uploads/2016/09/image5-768x310.png 768w, /wp-content/uploads/2016/09/image5.png 1024w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image5.png)

Add a **table** visual and add the following fields

  * Incident Dimension 
      * IncidentDIm_ID
      * Title
  * AffectedUserDim 
      * Company
      * Display Name
  * IncidentDim_IncidentClassification 
      * IncidentClassificationValue
  * IncidentDim_IncidentImpact 
      * IncidentImpactValue
  * IncidentDim_IncidentSource 
      * IncidentSourceValue
  * IndicentDim_IncidentStatus 
      * IncidentStatusValue

[<img class="alignnone size-medium wp-image-10971" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image6-300x53.png" alt="image6.png" width="300" height="53" srcset="/wp-content/uploads/2016/09/image6-300x53.png 300w, /wp-content/uploads/2016/09/image6-768x136.png 768w, /wp-content/uploads/2016/09/image6.png 1024w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image6.png)

Next we want to add a graphic showing us the amount of incidents per classification.

Add a **DonutChart** visual and add the following fields:

  * Legend 
      * IncidentClassificationValue
  * Primary Measure 
      * IncidentAffectedByUserCount

[<img class="alignnone size-medium wp-image-10991" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image7-300x156.png" alt="image7.png" width="300" height="156" srcset="/wp-content/uploads/2016/09/image7-300x156.png 300w, /wp-content/uploads/2016/09/image7-768x398.png 768w, /wp-content/uploads/2016/09/image7.png 1024w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image7.png)

## Final result

After a few hours digging around and playing with the visuals this is the final result:

[<img class="alignnone size-medium wp-image-11011" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image8-300x173.png" alt="image8.png" width="300" height="173" srcset="/wp-content/uploads/2016/09/image8-300x173.png 300w, /wp-content/uploads/2016/09/image8-768x442.png 768w, /wp-content/uploads/2016/09/image8.png 1024w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image8.png)

Pretty awesome!

# Publish to Power BI online

Now that we have created a report we can publish it to Power BI Service. I’d like to remind you again that you need to install and configure “<a href="http://biinsight.com/power-bi-enterprise-gateway-preview-episode-1/#dli" target="_blank">Power BI Enterprise Gateway</a>” on a machine in your network first.

  * Save the current Power BI Desktop report
  * Click “Publish” button form ribbon
  * Click “Sign in”

[<img class="alignnone size-medium wp-image-11031" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image9-300x47.png" alt="image9.png" width="300" height="47" srcset="/wp-content/uploads/2016/09/image9-300x47.png 300w, /wp-content/uploads/2016/09/image9-768x120.png 768w, /wp-content/uploads/2016/09/image9.png 1024w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image9.png)

Once published to Power BI online you don’t need to configure a refresh schedule if you are using “Connect Live” to query SSAS. Please keep in mind you need Power BI pro to be able use Live query as described here: [https://powerbi.microsoft.com/en-us/documentation/powerbi-refresh-data/](https://powerbi.microsoft.com/en-us/documentation/powerbi-refresh-data/ "https://powerbi.microsoft.com/en-us/documentation/powerbi-refresh-data/") The visualizations in your dashboard will query the on-premise Power BI gateway to connect to the local SSAS.

[<img class="alignnone size-medium wp-image-11051" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image10-300x174.png" alt="image10.png" width="300" height="174" srcset="/wp-content/uploads/2016/09/image10-300x174.png 300w, /wp-content/uploads/2016/09/image10-768x445.png 768w, /wp-content/uploads/2016/09/image10.png 780w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image10.png)

With the On-premises Data Gateway, you can issue queries from Power BI to your on-premises data sources. When you interact with a visualization, queries are sent from Power BI directly to the database. Updated data is then returned and visualizations are updated. Because there is a direct connection between Power BI and the database, there is no need to schedule refresh.

Thanks,

Alex
