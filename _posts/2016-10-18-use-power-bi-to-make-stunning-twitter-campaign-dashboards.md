---
id: 14561
title: Use Power BI to make stunning Twitter campaign dashboards
date: 2016-10-18T10:00:04+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=14561
sc_member_order:
  - "0"
  - "0"
  - "0"
bpxl_standard_excerpt_home:
  - "0"
  - "0"
bpxl_standard_single_hide:
  - "0"
  - "0"
bpxl_image_excerpt_home:
  - "0"
  - "0"
bpxl_image_single_hide:
  - "0"
  - "0"
bpxl_audio_excerpt_home:
  - "0"
  - "0"
bpxl_audio_single_hide:
  - "0"
  - "0"
bpxl_video_excerpt_home:
  - "0"
  - "0"
bpxl_video_single_hide:
  - "0"
  - "0"
bpxl_link_excerpt_home:
  - "0"
  - "0"
bpxl_link_single_hide:
  - "0"
  - "0"
bpxl_gallery_excerpt_home:
  - "0"
  - "0"
bpxl_gallery_single_hide:
  - "0"
  - "0"
bpxl_status_excerpt_home:
  - "0"
  - "0"
bpxl_status_single_hide:
  - "0"
  - "0"
bpxl_singlerelated:
  - "0"
  - "0"
post_views_count:
  - "4155"
  - "4155"
image: /wp-content/uploads/2016/10/dashboard1-150x150.png
categories:
  - Azure
tags:
  - Azure
  - Azure Functions
  - Power BI
---
As you all probably know by now, I&#8217;m a big fan of Power BI as it&#8217;s really a powerfull solution to analyze and visualize your data. I&#8217;m also a Twitter fan, so when I discovered there is a [Power BI solution ](https://powerbi.microsoft.com/en-us/solution-templates/brand-management-twitter/)that will track and analyze all of my unstructured Twitter data with a scalable dashboard solution, I just had to try this!

# Requirements

You will need the following components:

  * Power BI desktop
  * Azure subscription
  * Power BI Twitter solution

# Installation

The installation is pretty straight forward: Go to <https://powerbi.microsoft.com/en-us/solution-templates/brand-management-twitter/> and click on **Install now**

[<img class="alignnone size-large wp-image-14571" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-15-35-1024x843.png" alt="2016-10-14_11-15-35" width="768" height="632" srcset="/wp-content/uploads/2016/10/2016-10-14_11-15-35-1024x843.png 1024w, /wp-content/uploads/2016/10/2016-10-14_11-15-35-300x247.png 300w, /wp-content/uploads/2016/10/2016-10-14_11-15-35-768x632.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-15-35.png)

This brings up the next page where you can see how this solution works and what will be deployed in Azure:

  * A new Azure resource group
  * A Logical application that will connect to Twitter on a pre-defined schedule and launch a twitter search query. The output of this query will then be passed on to the next step
  * Azure Function that will use as input the twitter search query from our logicall application and store that data in a SQL database
  * A SQL database to store all of our twitter data
  * Power BI desktop file to visualize the Twitter data

[<img class="alignnone size-large wp-image-14581" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-16-06-1024x537.png" alt="2016-10-14_11-16-06" width="768" height="403" srcset="/wp-content/uploads/2016/10/2016-10-14_11-16-06-1024x537.png 1024w, /wp-content/uploads/2016/10/2016-10-14_11-16-06-300x157.png 300w, /wp-content/uploads/2016/10/2016-10-14_11-16-06-768x403.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-16-06.png)

On the next page, you need to connect to Azure. If you wish you can click **Advanced** to change the resource group

[<img class="alignnone size-large wp-image-14591" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-19-18-1024x469.png" alt="2016-10-14_11-19-18" width="768" height="352" srcset="/wp-content/uploads/2016/10/2016-10-14_11-19-18-1024x469.png 1024w, /wp-content/uploads/2016/10/2016-10-14_11-19-18-300x137.png 300w, /wp-content/uploads/2016/10/2016-10-14_11-19-18-768x352.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-19-18.png)

You can either create a new Azure SQL server or use an existing one.

[<img class="alignnone size-large wp-image-14601" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-23-30-1024x593.png" alt="2016-10-14_11-23-30" width="768" height="445" srcset="/wp-content/uploads/2016/10/2016-10-14_11-23-30-1024x593.png 1024w, /wp-content/uploads/2016/10/2016-10-14_11-23-30-300x174.png 300w, /wp-content/uploads/2016/10/2016-10-14_11-23-30-768x445.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-23-30.png)

Click **next**,  where you will have to provide your Twitter credentials and **authorize** Azure AppService Logic Apps to connect to twitter:

[<img class="alignnone size-large wp-image-14611" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-29-19-1024x878.png" alt="2016-10-14_11-29-19" width="768" height="659" srcset="/wp-content/uploads/2016/10/2016-10-14_11-29-19-1024x878.png 1024w, /wp-content/uploads/2016/10/2016-10-14_11-29-19-300x257.png 300w, /wp-content/uploads/2016/10/2016-10-14_11-29-19-768x658.png 768w, /wp-content/uploads/2016/10/2016-10-14_11-29-19.png 1071w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-29-19.png)

Click **next. **Now you will have to define the search terms that you are interested in. So I&#8217;m interested in Azure, OMS and Power Bi related hashtags so I would put in:

<pre class="lang:default decode:true ">#Azure OR #MSPOWERBI OR #MSOMS</pre>

You can find more about Twitter search queries [here](https://dev.twitter.com/rest/public/search).

[<img class="alignnone size-large wp-image-14631" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-32-39-1024x425.png" alt="2016-10-14_11-32-39" width="768" height="319" srcset="/wp-content/uploads/2016/10/2016-10-14_11-32-39-1024x425.png 1024w, /wp-content/uploads/2016/10/2016-10-14_11-32-39-300x124.png 300w, /wp-content/uploads/2016/10/2016-10-14_11-32-39-768x319.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-32-39.png)

You can enrich the dashboard with the tweet direction for a specific Twitter handle (like your own). So you can track inbound and outbound tweets.

[<img class="alignnone size-large wp-image-14641" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-33-59-1024x461.png" alt="2016-10-14_11-33-59" width="768" height="346" srcset="/wp-content/uploads/2016/10/2016-10-14_11-33-59-1024x461.png 1024w, /wp-content/uploads/2016/10/2016-10-14_11-33-59-300x135.png 300w, /wp-content/uploads/2016/10/2016-10-14_11-33-59-768x346.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-33-59.png)

Lastly, you can verify if all the parameters are correct and click **Run**.

<img class="alignnone size-full wp-image-14921" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-34-19.png" alt="2016-10-14_11-34-19" width="2160" height="969" /> 

The deployment will take about 15 minutes to complete, make sure you don&#8217;t close your browser until all the steps are completed.

[<img class="alignnone size-large wp-image-14661" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-35-07-1024x623.png" alt="2016-10-14_11-35-07" width="768" height="467" srcset="/wp-content/uploads/2016/10/2016-10-14_11-35-07-1024x623.png 1024w, /wp-content/uploads/2016/10/2016-10-14_11-35-07-300x183.png 300w, /wp-content/uploads/2016/10/2016-10-14_11-35-07-768x468.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-35-07.png)

Once completed, all you have to do is **download the PBIX ** file, which will open Power Bi desktop.

[<img class="alignnone size-large wp-image-14681" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-44-49-1024x637.png" alt="2016-10-14_11-44-49" width="768" height="478" srcset="/wp-content/uploads/2016/10/2016-10-14_11-44-49-1024x637.png 1024w, /wp-content/uploads/2016/10/2016-10-14_11-44-49-300x187.png 300w, /wp-content/uploads/2016/10/2016-10-14_11-44-49-768x478.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-44-49.png)

We are almost there, just one last step 😀.

Once Power Bi desktop is open you will have to enter the SQL credentials before you can start exploring your data. Please select **Edit Queries **in the top ribbon, under the **Home** tab.

<div>
  You should see an <b>Edit Credentials </b>message in the yellow bar. Select it and make sure you are in the <b>Database </b>tab (as opposed to the <b>Windows</b> tab).
</div>

[<img class="alignnone size-large wp-image-14751" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/cred-1024x560.png" alt="cred" width="768" height="420" srcset="/wp-content/uploads/2016/10/cred-1024x560.png 1024w, /wp-content/uploads/2016/10/cred-300x164.png 300w, /wp-content/uploads/2016/10/cred-768x420.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/cred.png)

Enter the credentials to connect to your Azure SQL database and click **Connect**

<img class="alignnone size-full wp-image-14961" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_11-49-36.png" alt="2016-10-14_11-49-36" width="1049" height="470" srcset="/wp-content/uploads/2016/10/2016-10-14_11-49-36.png 1049w, /wp-content/uploads/2016/10/2016-10-14_11-49-36-300x134.png 300w, /wp-content/uploads/2016/10/2016-10-14_11-49-36-768x344.png 768w, /wp-content/uploads/2016/10/2016-10-14_11-49-36-1024x459.png 1024w" sizes="(max-width: 1049px) 100vw, 1049px" /> 

Data should now start coming into your Power BI file! It can take a few minutes for the first tweets to appear.

[<img class="alignnone size-large wp-image-14771" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/dashboard1-1024x541.png" alt="dashboard1" width="768" height="406" srcset="/wp-content/uploads/2016/10/dashboard1-1024x541.png 1024w, /wp-content/uploads/2016/10/dashboard1-300x159.png 300w, /wp-content/uploads/2016/10/dashboard1-768x406.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/dashboard1.png)  
Pretty awesome he! 🙂

Go to the Azure Portal if you would like to change the polling interval or the Twitter hashtags, and open the Logical app and click the **Logical App designer**. In here you will be able to change the hash tags if required as shown below

[<img class="alignnone size-large wp-image-14721" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_12-18-49-1024x524.png" alt="2016-10-14_12-18-49" width="768" height="393" srcset="/wp-content/uploads/2016/10/2016-10-14_12-18-49-1024x524.png 1024w, /wp-content/uploads/2016/10/2016-10-14_12-18-49-300x154.png 300w, /wp-content/uploads/2016/10/2016-10-14_12-18-49-768x393.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/2016-10-14_12-18-49.png)

That&#8217;s it!

As you can see it was relatively easy to install and start analyzing my Twitter feeds. I also made a short video of the solution here:



You can also test the dashboard <a href="https://app.powerbi.com/view?r=eyJrIjoiYjNmYjliMjktMzAyZS00MTRkLWJlMGEtNGE5NzYxOWQwODM0IiwidCI6IjU3NGMzZTU2LTQ5MjQtNDAwNC1hZDFhLWQ4NDI3ZTdkYjI0MSIsImMiOjZ9" target="_blank">here</a>.

The more time I spend in Power BI, the more I&#8217;m impressed by its capabilities!

What kind of data would you like to visualize with Power BI?

Thanks,

Alexandre

&nbsp;

&nbsp;
