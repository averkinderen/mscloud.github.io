---
id: 19693
title: Export SQL reports in PDF landscape
date: 2009-09-03T12:53:00+10:00
author: alexandre@verkinderen.com
layout: post
guid: /blogs/scom/archive/2009/09/03/export-sql-reports-in-pdf-landscape.aspx
permalink: /export-sql-reports-in-pdf-landscape/
sc_member_order:
  - "0"
  - "0"
post_views_count:
  - "4233"
categories:
  - SystemCenter
  - Uncategorized
tags:
  - Issue
  - opsmgr
  - opsmgr R2
  - reporting
  - scom
  - sql
---
I had to create some reports for a customer this week and the layout of the report didn&rsquo;t satisfied my client. The reports are exported in portrait format and not in landscape format.

&nbsp;

First part of the report

[<img height="184" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_43A1B614.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_127FEAC3.png)

and on the second page I got the rest of my report.

[<img height="244" width="187" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_1818281E.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_00C5719A.png)

&nbsp;

Very ugly&hellip;&hellip;&hellip;.

<img height="79" width="105" src="http://www.midwestrocklobster.com/ugly/ugly3_lg.gif" /> 

&nbsp;

### How to export a scom report in pdf landscape format?

&nbsp;Only solution here is to render the pdf in landscape format, so I start googling and found this blog [http://www.bictt.com/blogs/bictt.php/2009/03/17/sql-reporting-services-render-pdf-in-a4-1](http://www.bictt.com/blogs/bictt.php/2009/03/17/sql-reporting-services-render-pdf-in-a4-1 "http://www.bictt.com/blogs/bictt.php/2009/03/17/sql-reporting-services-render-pdf-in-a4-1")&nbsp; and also some information msdn [http://msdn.microsoft.com/en-us/library/ms156281.aspx](http://msdn.microsoft.com/en-us/library/ms156281.aspx "http://msdn.microsoft.com/en-us/library/ms156281.aspx")&nbsp;

&nbsp;

So to resolve our problem we have to add some code in the Rsreportserver.config file that you can find under &ldquo;Program FilesMicrosoft SQL ServerMSSQL.5Reporting ServicesReportServer&rdquo;

&nbsp;

You can specify rendering extension parameters in the RSReportServer configuration file to override default report rendering behavior for reports that run on a Reporting Services report server. You can modify rendering extension parameters to achieve the following objectives:

  * Change how the rendering extension name appears in the Export list of the report toolbar (for example, to change &#8220;Web archive&#8221; to &#8220;MHTML&#8221;), or localize the name to a different language. 
  * Create multiple instances of the same rendering extension to support different report presentation options (for example, a portrait and landscape mode version of the Image rendering extension). 
  * Change the default rendering extension parameters to use different values (for example, the Image rendering extension uses TIFF as the default output format; you can modify the extension parameters to use EMF instead). 

&nbsp;

Locate the render section in the rsreportserver.config file

&nbsp;[<img height="31" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/Capture_thumb_1D1F872F.png" alt="Capture" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/Capture_108F4962.png)

&nbsp;

We are going to add two extra entries to the export list.

Below the pdf entry paste the following code:

`<Extension Name="PDF (A4 Landscape)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.PdfReport,Microsoft.ReportingServices.ImageRendering">`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <OverrideNames>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <Name Language="en-US">PDF in A4 Landscape</Name>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </OverrideNames>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <Configuration>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <DeviceInfo>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <OutputFormat>PDF</OutputFormat>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <PageHeight>8.27in</PageHeight>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <PageWidth>11.69in</PageWidth>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </DeviceInfo>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </Configuration>`

`</Extension>`

`<Extension Name="PDF (A4 Portrait)" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.PdfReport,Microsoft.ReportingServices.ImageRendering">`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <OverrideNames>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <Name Language="en-US">PDF in A4 Portrait</Name>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </OverrideNames>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <Configuration>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <DeviceInfo>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <OutputFormat>PDF</OutputFormat>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <PageHeight>11.69in</PageHeight>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <PageWidth>8.27in</PageWidth>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </DeviceInfo>`

`&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </Configuration>`

`</Extension>`

``

Save the file and close it. I also did a IIsreset and a restart of my sql reporting services just to be sure.

When I want to export a report I have two extra entries:

[<img height="135" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_212EF663.png" alt="image" border="0" style="border-right-width: 0px;border-top-width: 0px;border-bottom-width: 0px;border-left-width: 0px" />](http://scug.be/scom/files/2012/06/image_73AB45EE.png)

&nbsp;

Now when I want to export a report in landscape format I just choose to export in pdf in A4 landscape format and this is the result:

[<img height="167" width="244" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_thumb_7F234844.png" alt="image" border="0" style="border-bottom: 0px;border-left: 0px;border-top: 0px;border-right: 0px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage//2012/06/image_67424427.png)

&nbsp;

Everything perfectly fits&nbsp;on one page and I have a happy client now 🙂 !!&nbsp; Thanks to **Bob Cornelissen** for his blog.

&nbsp;

Hope this helps,

Alexandre Verkinderen