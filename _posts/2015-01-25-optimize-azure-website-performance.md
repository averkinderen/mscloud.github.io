---
id: 5051
title: Optimize Azure website performance
date: 2015-01-25T14:51:16+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=5051
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
  - "11017"
  - "11017"
  - "11017"
image: /wp-content/uploads/2015/01/graph-150x150.png
categories:
  - Azure
tags:
  - Azure
  - end to end monitoring
  - Performance
  - websites
---
A couple of weeks ago I moved my blog to a new wordpress site hosted in Azure. The deployment of the WordPress website was very smooth but I was not happy about the performance 🙁 So I started my investigation on how I could optimize Azure website performance.

If your WordPress site is slow then check for these:

### Do not deploy on Free or Shared service tiers

**Free tier or shared** are not sufficient for running a production site and hence you need to upgrade to Basic or Standard Tier. Check out the features supported for each tier and select the appropriate Tier, [Azure Websites Pricing per tier](http://azure.microsoft.com/en-us/pricing/details/web-sites/).

#### Service Tiers

The Azure Websites service is available in Free, Shared, Basic and Standard editions. The Free tier allows you to host up to 10 Websites in a shared environment. Basic and Standard tiers run your web apps in private Virtual Machines which are dedicated to your apps. You can host multiple websites/domains in each Basic and Standard instance you deploy.

|                                | FREE                 | SHARED                                                                                                                                                               | BASIC                                                                                                                                                                | STANDARD                                   |
| ------------------------------ | -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| Number of unique websites/apps | 10                   | 100                                                                                                                                                                  | Unlimited                                                                                                                                                            | Unlimited                                  |
| Disk Space                     | 1 GB                 | 1 GB                                                                                                                                                                 | 10 GB                                                                                                                                                                | 50 GB                                      |
| Maximum daily bandwidth        | Up to 165 MB per day | Up to 165 MB per day                                                                                                                                                 | Unlimited                                                                                                                                                            | Unlimited                                  |
| Custom DNS domain support      | &#8212;              |                                                                                                                                                                      |                                                                                                                                                                      |                                            |
| SSL certificate support        | &#8212;              | <a title="" href="http://azure.microsoft.com/en-us/pricing/details/websites/#ssl-connections" data-tab-id="2" data-tab-panel="tabs-services">SSL pricing applies</a> | <a title="" href="http://azure.microsoft.com/en-us/pricing/details/websites/#ssl-connections" data-tab-id="2" data-tab-panel="tabs-services">SSL pricing applies</a> | 5 SNI SSL and 1 IP SSL included at no cost |
| Maximum VM instances           | &#8212;              | 1 shared instances                                                                                                                                                   | 3 dedicated VM instances                                                                                                                                             | 10 dedicated VM instances                  |
| Autoscale support              | &#8212;              | &#8212;                                                                                                                                                              |                                                                                                                                                                      |                                            |
| Staged Publishing Slots        | &#8212;              | &#8212;                                                                                                                                                              | 1 slot per site                                                                                                                                                      | 5 slots per site                           |
| Web sockets                    | 5 connections        | 35 connections                                                                                                                                                       | 350 connections                                                                                                                                                      | Unlimited                                  |
| Automated Backups              | &#8212;              | &#8212;                                                                                                                                                              | &#8212;                                                                                                                                                              |                                            |
| Global Traffic Management      | &#8212;              | &#8212;                                                                                                                                                              | &#8212;                                                                                                                                                              |                                            |
| SLA                            | Not available        | Not available                                                                                                                                                        | 99.95%                                                                                                                                                               | 99.95%                                     |

&nbsp;

### Is your website unloading after a while?

By default, websites are unloaded if they are idle for some period of time. This lets the system conserve resources. In Basic or Standard mode, you can enable **Always On** to keep the site loaded all the time. If your site runs continuous web jobs, you should enable **Always On**, or the web jobs may not run reliably.

[<img class="alignnone size-medium wp-image-5082" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/alwayson-276x300.png" alt="alwayson" width="276" height="300" srcset="/wp-content/uploads/2015/01/alwayson-276x300.png 276w, /wp-content/uploads/2015/01/alwayson-768x835.png 768w, /wp-content/uploads/2015/01/alwayson.png 896w" sizes="(max-width: 276px) 100vw, 276px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/alwayson.png)

&nbsp;

### Make sure your website and database are running in the same Region

If your website is setup in say West US and your database is setup in say East US ; then this can impact performance of the website as both these components are in different datacenters and network latency for the database calls can add to your page load time. Make sure your website and database are in the same regions/data centers.

You can verify the location of your website on the dashboard page

[<img class="alignnone size-full wp-image-5141" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/web.png" alt="web" width="278" height="248" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/web.png)

and the location of the database you need to verify in the cleardb management webpage:

[<img class="alignnone size-medium wp-image-5151" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/cleardblocation-300x160.png" alt="cleardblocation" width="300" height="160" srcset="/wp-content/uploads/2015/01/cleardblocation-300x160.png 300w, /wp-content/uploads/2015/01/cleardblocation-768x410.png 768w, /wp-content/uploads/2015/01/cleardblocation.png 945w" sizes="(max-width: 300px) 100vw, 300px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/cleardblocation.png)

### Are your using a Free ClearDB MySQL database?

The Free ClearDB MySQL database is not a production website.

&nbsp;

[<img class="alignnone size-medium wp-image-5061" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/cleardb-300x123.png" alt="cleardb" width="300" height="123" srcset="/wp-content/uploads/2015/01/cleardb-300x123.png 300w, /wp-content/uploads/2015/01/cleardb-768x316.png 768w, /wp-content/uploads/2015/01/cleardb.png 911w" sizes="(max-width: 300px) 100vw, 300px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/cleardb.png)

&nbsp;

Immediately after upgrading my ClearDB I noticed a huge performance gain!

## Monitoring endpoints

Now that we have optimized the website performance let&#8217;s monitor the response time! Monitoirng endpoints feature, available in **Standard** mode, lets you monitor up to 2 endpoints from up to 3 geographic locations.

Endpoint monitoring configures web tests from geo-distributed locations that test response time and uptime of web URLs. The test performs an HTTP get operation on the web URL to determine the response time and uptime from each location. Each configured location runs a test every five minutes.

Uptime is monitored using HTTP response codes, and response time is measured in milliseconds. Uptime is considered 100% when the response time is less than 30 seconds and the HTTP status code is lower than 400. Uptime is 0% when the response time is greater than 30 seconds or the HTTP status code is greater than 400.

After you configure endpoint monitoring, you can drill down into the individual endpoints to view details response time and uptime status over the monitoring interval from each of the test locations. You can also set up an alert rule when the endpoint takes too long to respond, for example.

**To configure endpoint monitoring:**

  1. Open **Websites**. Click the name of the website you want to configure.
  2. Click the **Configure** tab.
  3. Go to the **Monitoring** section to enter your endpoint settings.
  4. Enter a name for the endpoint.
  5. Enter the URL for a part of your website that you want to monitor. For example, http://mscloud.be .
  6. Select one or more geographic locations from the list.
  7. Optionally, repeat the previous steps to create a second endpoint.
  8. Click **Save**. It may take some time for the web endpoint monitoring data to be available on the **Dashboard** and **Monitor** tabs.

<img class="alignnone size-medium wp-image-5101" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/endpoints-300x108.png" alt="endpoints" width="300" height="108" srcset="/wp-content/uploads/2015/01/endpoints-300x108.png 300w, /wp-content/uploads/2015/01/endpoints-768x277.png 768w, /wp-content/uploads/2015/01/endpoints.png 911w" sizes="(max-width: 300px) 100vw, 300px" /> 

Go to the monitoring tab and you will after a while see the first response time of 3 different locations for your website!

[<img class="alignnone size-medium wp-image-5131" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/graph-300x148.png" alt="graph" width="300" height="148" srcset="/wp-content/uploads/2015/01/graph-300x148.png 300w, /wp-content/uploads/2015/01/graph-768x378.png 768w, /wp-content/uploads/2015/01/graph.png 946w" sizes="(max-width: 300px) 100vw, 300px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/graph.png)

&nbsp;

##  Conclusion

The free or share website instacnce together with the free MysqlDB are not a solution for production websites.

Kind regards,

Alexandre

&nbsp;
