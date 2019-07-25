---
id: 18451
title: Microsoft PowerApps and inner join 2 sql tables
date: 2017-03-08T15:27:57+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=18451
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
  - "12077"
  - "12077"
  - "12077"
  - "12077"
image: /wp-content/uploads/2017/03/powerappslogo-150x150.jpg
categories:
  - Azure
tags:
  - Azure
  - Azure SQL
  - cubesys
  - PowerApps
  - sql
---
Since I was testing and discovering <a href="https://powerapps.microsoft.com/en-us/" target="_blank">Microsoft  PowerApps</a> I wanted to create a new app that would be able to create new invoices and expenses from my mobile phone. To be able to do this I would need to link 2 different data sources (in my case 2 different SQL tables) together and perform an inner join or something similar. At present, this is something that is not clearly documented, hence this blogpost.

## Backend infrastructure

First of all let&#8217;s build the required backend to support my test application.

I quickly created a SQL database hosted in Azure with couple of tables and foreign key relationships. For example in my invoice table I would have a ContractorID column with a relationship to the Contractor table containing more information regarding the contractors.

<img class="alignnone size-full wp-image-18561" src="http://www.mscloud.be/wp-content/uploads/2017/03/sqldiagram.png" alt="sqldiagram" width="1724" height="1187" srcset="/wp-content/uploads/2017/03/sqldiagram.png 1724w, /wp-content/uploads/2017/03/sqldiagram-300x207.png 300w, /wp-content/uploads/2017/03/sqldiagram-768x529.png 768w, /wp-content/uploads/2017/03/sqldiagram-1024x705.png 1024w" sizes="(max-width: 1724px) 100vw, 1724px" /> 

## Build your app in PowerApps

Now that we have our backed database we can start building our PowerApp. First sign up to PowerApps through your Office365 subscription or follow this tutorial: <a href="https://powerapps.microsoft.com/en-us/tutorials/signup-for-powerapps/" target="_blank">https://powerapps.microsoft.com/en-us/tutorials/signup-for-powerapps/</a>

Once you are signed up, to build your new app go to <a href="https://web.powerapps.com" target="_blank">https://web.powerapps.com</a> and click new App.

<img class="alignnone size-full wp-image-18791" src="http://www.mscloud.be/wp-content/uploads/2017/03/file-new.png" alt="file-new" width="103" height="174" /> 

In PowerApp you can retrieve data and <a href="https://powerapps.microsoft.com/en-us/tutorials/connections-list/" target="_blank">make connections </a>to a large number of different sources like Office 365, Dropbox, Twitter, and other common SaaS and enterprise services. We are going to create a new connection to our SQL server that is running in Azure and select our invoice table.

<img class="alignnone size-full wp-image-18541" src="http://www.mscloud.be/wp-content/uploads/2017/03/dataset.png" alt="dataset" width="1073" height="1031" srcset="/wp-content/uploads/2017/03/dataset.png 1073w, /wp-content/uploads/2017/03/dataset-300x288.png 300w, /wp-content/uploads/2017/03/dataset-768x738.png 768w, /wp-content/uploads/2017/03/dataset-1024x984.png 1024w" sizes="(max-width: 1073px) 100vw, 1073px" /> 

PowerApps will then start building your app based on that table and will create 3 views by default: 1 browse screen, 1 edit and a new item screen.

[<img class="alignnone size-large wp-image-18911" src="http://www.mscloud.be/wp-content/uploads/2017/03/browse-1-1024x860.png" alt="" width="768" height="645" />](http://www.mscloud.be/wp-content/uploads/2017/03/browse-1.png)

As you can see above my app is not showing me the data of my other tables, it&#8217;s just showing me the foreign key ID&#8217;s. To be able to show data from the other tables you have to add the other tables as separate data sources:

  * In the right-hand pane, click or tap the **Data sources** tab, and then click or tap **Add data source**.
  * If the right-hand pane doesn&#8217;t show a **Data sources** tab, click or tap any screen in the left navigation bar.

[<img class="alignnone size-full wp-image-18881" src="http://www.mscloud.be/wp-content/uploads/2017/03/newdatasource.png" alt="" width="264" height="189" />](http://www.mscloud.be/wp-content/uploads/2017/03/newdatasource.png)

[<img class="alignnone wp-image-18671 size-medium" src="http://www.mscloud.be/wp-content/uploads/2017/03/datasource-91x300.png" alt="" width="91" height="300" srcset="/wp-content/uploads/2017/03/datasource-91x300.png 91w, /wp-content/uploads/2017/03/datasource-311x1024.png 311w, /wp-content/uploads/2017/03/datasource.png 364w" sizes="(max-width: 91px) 100vw, 91px" />](http://www.mscloud.be/wp-content/uploads/2017/03/datasource.png)

## Linking 2 PowerApps data sources

Now that I have my different datasources in PowerApps I looked up how to inner join data from 2 different SQL tables expecting I could use inner joins just like in SQL. However at the time of writing you cannot use inner joins at all! Hopefully this feature will come very soon.

Despite searching everywhere on the internet on how to link 2 SQL tables with an inner join together I couldn&#8217;t find any relevant information on how to do it. The only chance I had was to see if I could achieve my inner join with the LookUp function in PowerApps. The LookUp function finds the first record in a table that satisfies a formula. Use LookUp to find a single record that matches one or more criteria.

**LookUp**( _Table_, _Formula_ [, _ReductionFormula_ ] )

  * _Table_ &#8211; Required. Table to search.

This would be in my case **&#8220;dbo.Contractor&#8221;** as I wanted to find the contractor name in the contractor table.

  * _Formula_ &#8211; Required. This formula is evaluated for each record of the table, and the first record that results in **true** is returned. You can reference columns within the table.

For the formula I wanted to compare the ID within the contractor table with the ID of **This Item**. So I used: &#8220;ID=ThisItem.ContractorID&#8221;

  * _ReductionFormula_ &#8211; Optional. This formula is evaluated over the record that was found, reducing the record to a single value. You can reference columns within the table. If this parameter is not supplied, the function returns the full record from the table.

And I only wanted to see the name of the contractor, not the whole record, so I specified **Name** for the reduction formula. This is the final formula:

&nbsp;

<pre class="lang:tsql decode:true">LookUp('[dbo].[contractor]',ID=ThisItem.contractor,Name)</pre>

To change the displayed text, click on the text box and change the formula from this:

[<img class="alignnone wp-image-19011 size-medium" src="http://www.mscloud.be/wp-content/uploads/2017/03/contractorid-300x104.png" alt="" width="300" height="104" srcset="/wp-content/uploads/2017/03/contractorid-300x104.png 300w, /wp-content/uploads/2017/03/contractorid-768x266.png 768w, /wp-content/uploads/2017/03/contractorid.png 985w" sizes="(max-width: 300px) 100vw, 300px" />](http://www.mscloud.be/wp-content/uploads/2017/03/contractorid.png)

To this:

[<img class="alignnone wp-image-19001 size-medium" src="http://www.mscloud.be/wp-content/uploads/2017/03/contractor-300x107.png" alt="" width="300" height="107" srcset="/wp-content/uploads/2017/03/contractor-300x107.png 300w, /wp-content/uploads/2017/03/contractor-768x274.png 768w, /wp-content/uploads/2017/03/contractor.png 957w" sizes="(max-width: 300px) 100vw, 300px" />](http://www.mscloud.be/wp-content/uploads/2017/03/contractor.png)

This is the final result with all the fields changed:

[<img class="alignnone wp-image-18981 size-large" src="http://www.mscloud.be/wp-content/uploads/2017/03/linksok-1024x326.png" alt="" width="768" height="245" srcset="/wp-content/uploads/2017/03/linksok-1024x326.png 1024w, /wp-content/uploads/2017/03/linksok-300x95.png 300w, /wp-content/uploads/2017/03/linksok-768x244.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](http://www.mscloud.be/wp-content/uploads/2017/03/linksok.png)

&nbsp;

Hope this helps,

Alexandre Verkinderen
