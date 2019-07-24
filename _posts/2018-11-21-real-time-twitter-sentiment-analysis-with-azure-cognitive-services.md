---
id: 19898
title: Real Time Twitter sentiment analysis with Azure Cognitive Services
date: 2018-11-21T10:16:53+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://mscloud.be/?p=19898
permalink: /real-time-twitter-sentiment-analysis-with-azure-cognitive-services/
sc_member_order:
  - "0"
bpxl_standard_excerpt_home:
  - "0"
bpxl_standard_single_hide:
  - "0"
bpxl_image_excerpt_home:
  - "0"
bpxl_image_single_hide:
  - "0"
bpxl_audio_excerpt_home:
  - "0"
bpxl_audio_single_hide:
  - "0"
bpxl_video_excerpt_home:
  - "0"
bpxl_video_single_hide:
  - "0"
bpxl_link_excerpt_home:
  - "0"
bpxl_link_single_hide:
  - "0"
bpxl_gallery_excerpt_home:
  - "0"
bpxl_gallery_single_hide:
  - "0"
bpxl_status_excerpt_home:
  - "0"
bpxl_status_single_hide:
  - "0"
bpxl_singlerelated:
  - "0"
post_views_count:
  - "2850"
categories:
  - Azure
tags:
  - Azure
  - Logic Apps
  - Power BI
  - Twitter
---
I was recently playing with Azure Cognitive Services and wanted to test Sentiment Analysis of Twitter. In this blog post I will go through how to setup the different components and analyse the sentiment of Tweets that contain the Azure or AWS hashtag. We will then be able to compare the sentiment of Azure tweets versus AWS tweets and analyse if Azure is in a better spotlight than AWS, which country prefers AWS over Azure, get the most influential people, and many more things that would be hugely beneficial for any social media marketing team.

For this solution to work we will need the following Azure Services:

  1. Azure Logic Apps to collect and read Tweets with a certain hashtag
  2. Azure Cognitive Services to analyse the sentiment in the tweet
  3. Azure SQL DB to store the tweet and the sentiment
  4. Power Bi to to visualise the sentiment

Granted, I could have skipped the database step and stream from logic apps directly into Power BI but that will be for another blogpost.

### Azure SQL DB

First create a new Azure SQL DB and open the query editor to create the table:

[<img class="alignnone size-medium wp-image-19899" src="/wp-content/uploads/2018/11/queryeditor-300x182.png" alt="" width="300" height="182" srcset="/wp-content/uploads/2018/11/queryeditor-300x182.png 300w, /wp-content/uploads/2018/11/queryeditor.png 560w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/11/queryeditor.png)

Run the following SQL query to create the table for Azure

<pre class="lang:mysql decode:true">CREATE TABLE AzureTweets (

id int PRIMARY KEY IDENTITY,

createdDate datetime DEFAULT(getdate()),

tweettext varchar(512) SPARSE NULL,

sentiment Float NULL,

author VARCHAR (512) ,

location VARCHAR (512) ,

);</pre>

I then run the same command to have a table for AWS tweets.

<pre class="lang:mysql decode:true ">CREATE TABLE AWSTweets (

id int PRIMARY KEY IDENTITY,

createdDate datetime DEFAULT(getdate()),

tweettext varchar(512) SPARSE NULL,

sentiment Float NULL,

author VARCHAR (512) ,

location VARCHAR (512) ,

);</pre>

&nbsp;

### Cognitive Services key

We will need Azure Cognitive services to analyse our Tweet and detect the sentiment of the tweet. The Text Analytics API, which is part of the Cognitive services, is a cloud-based service that provides advanced natural language processing over raw text has 3 main components: sentiment analysis, key phrase extraction, and language detection. There is a 4th component which is in preview now called Entity recognition which identifies and categorize entities in your text as people, places, organizations, date/time, quantities, percentages, currencies, and more. Well-known entities are also recognized and linked to more information on the web.

For this blog post we will focus on the Sentiment analysis which uses a machine learning classification algorithm to generate a sentiment score between 0 and 1. Scores closer to 1 indicate positive sentiment, while scores closer to 0 indicate negative sentiment. The model is pretrained with an extensive body of text with sentiment associations. Currently, it is not possible to provide your own training data. Currently, Sentiment Analysis supports English, German, Spanish, and French. Other languages are in preview. Sentiment analysis produces a higher quality result when you give it smaller chunks of text to work on. This is opposite from key phrase extraction, which performs better on larger blocks of text. ou must have JSON documents in this format: id, text, language and document size must be under 5,000 characters per document, which is not an issue for our Tweets. From a pricing point of view its literally a few cents per 1000 API requests.

[<img class="alignnone size-medium wp-image-19916" src="/wp-content/uploads/2018/11/pricing-203x300.png" alt="" width="203" height="300" srcset="/wp-content/uploads/2018/11/pricing-203x300.png 203w, /wp-content/uploads/2018/11/pricing.png 569w" sizes="(max-width: 203px) 100vw, 203px" />](/wp-content/uploads/2018/11/pricing.png)

We will need an API key for the logica app to connect to Azure cognitive services. Get the key for the Text Analysis API here: <https://azure.microsoft.com/en-us/try/cognitive-services/my-apis/?api=text-analytics>

### Azure Logic App

Create a new blank Azure Logic app. Edit the workflow of the logic app in the logic app designer. Click the “new step” button and add three actions.

  1. First we need to collect the Azure related tweets
  2. then we need to analyze the sentiment
  3. and lastly we will store the tweet with the sentiment in our SQL database

If you click the Twitter step, it will ask you to configure a connection to Twitter. Specify your credentials. Then enter the appropriate values regarding keywords and interval. I set the interval to 3 Minutes and specify the #Azure hashtag. If you want near real time analysis you should lower this value but the more actions are executed the more you [will pay.](https://azure.microsoft.com/en-au/pricing/details/logic-apps/)

[<img class="alignnone size-medium wp-image-19900" src="/wp-content/uploads/2018/11/logicapp-300x75.png" alt="" width="300" height="75" srcset="/wp-content/uploads/2018/11/logicapp-300x75.png 300w, /wp-content/uploads/2018/11/logicapp-768x193.png 768w, /wp-content/uploads/2018/11/logicapp-1024x258.png 1024w, /wp-content/uploads/2018/11/logicapp.png 1320w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/11/logicapp.png)

Next add the sentiment action to the workflow.  First you have to specify the keys you created earlier and give the new connection a name. Then you need to specify the &#8220;Tweet Text&#8221; from Dynamic content

[<img class="alignnone size-medium wp-image-19901" src="/wp-content/uploads/2018/11/detect-300x167.png" alt="" width="300" height="167" srcset="/wp-content/uploads/2018/11/detect-300x167.png 300w, /wp-content/uploads/2018/11/detect.png 726w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/11/detect.png)

As a result of this we will now have a sentiment, or a value ranging from 0 to 1, that we can insert in our database. Add a new action to insert a row in the database. Establish a connection to a specific database first.  Then specify the table (AzureTweets, in my case) and pass the values , again taken from the dynamic content like the Tweet Text, the author, location and sentiment.

[<img class="alignnone size-medium wp-image-19903" src="/wp-content/uploads/2018/11/sql-1-300x210.png" alt="" width="300" height="210" srcset="/wp-content/uploads/2018/11/sql-1-300x210.png 300w, /wp-content/uploads/2018/11/sql-1-768x537.png 768w, /wp-content/uploads/2018/11/sql-1.png 912w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/11/sql-1.png)

Click Save and Run.

After a while you should see some tweets coming into our database:

[<img class="alignnone size-medium wp-image-19931" src="/wp-content/uploads/2018/11/dbresults-300x134.png" alt="" width="300" height="134" srcset="/wp-content/uploads/2018/11/dbresults-300x134.png 300w, /wp-content/uploads/2018/11/dbresults-768x343.png 768w, /wp-content/uploads/2018/11/dbresults-1024x458.png 1024w, /wp-content/uploads/2018/11/dbresults.png 1255w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/11/dbresults.png)

Do the same steps mentioned above for AWS.

### Power Bi

Now that we have our tweets and sentiment in our SQL Database we can create a nice looking dashboard to visualize the sentiment.

In Power BI click “Get Data” and pick “Azure SQL Database”.

[<img class="alignnone size-medium wp-image-19904" src="/wp-content/uploads/2018/11/data-300x192.png" alt="" width="300" height="192" srcset="/wp-content/uploads/2018/11/data-300x192.png 300w, /wp-content/uploads/2018/11/data-768x491.png 768w, /wp-content/uploads/2018/11/data-1024x654.png 1024w, /wp-content/uploads/2018/11/data-570x365.png 570w, /wp-content/uploads/2018/11/data.png 1355w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/11/data.png)

Specify servername and database name and choose “Direct Query”. This way the data shown by the report is taken directly from the database

[<img class="alignnone size-medium wp-image-19905" src="/wp-content/uploads/2018/11/directquery-300x148.png" alt="" width="300" height="148" srcset="/wp-content/uploads/2018/11/directquery-300x148.png 300w, /wp-content/uploads/2018/11/directquery-768x380.png 768w, /wp-content/uploads/2018/11/directquery.png 783w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/11/directquery.png)

Press “advanced options” to be able to run a T-SQL query on the data to adjust it before using it in your report.

[<img class="alignnone size-medium wp-image-19906" src="/wp-content/uploads/2018/11/query-300x293.png" alt="" width="300" height="293" srcset="/wp-content/uploads/2018/11/query-300x293.png 300w, /wp-content/uploads/2018/11/query-55x55.png 55w, /wp-content/uploads/2018/11/query.png 681w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/11/query.png)

Now that we have the data in Power Bi we can start building our dashboard.

If you don&#8217;t already have the Word Cloud custom visual installed, install it. In the Visualizations panel to the right of the workspace, click the three dots (**&#8230;**) and choose **Import From Store**. Then search for &#8220;cloud&#8221; and click the **Add** button next the Word Cloud visual. Power BI installs the Word Cloud visual and lets you know that it installed successfully.

First, click the Word Cloud icon in the Visualizations panel. A new report appears in the workspace. Drag the `Tweet` field from the Fields panel to the Category field in the Visualizations panel. The word cloud appears inside the report. Now switch to the Format page of the Visualizations panel. In the Stop Words category, turn on **Default Stop Words** to eliminate short, common words like &#8220;of&#8221; from the cloud.

Now create a “Line and clustered column chart” as seen below. Activate the values “datebasedbyhour” and “id” and “sentiment” as shown below. Make sure you’re using “Average of sentiment” (not sum) as column value and Count of id (not sum) as a line value.

[<img class="alignnone size-medium wp-image-19932" src="/wp-content/uploads/2018/11/line-300x201.png" alt="" width="300" height="201" srcset="/wp-content/uploads/2018/11/line-300x201.png 300w, /wp-content/uploads/2018/11/line-768x515.png 768w, /wp-content/uploads/2018/11/line.png 891w" sizes="(max-width: 300px) 100vw, 300px" />](/wp-content/uploads/2018/11/line.png)

Next add the &#8220;Filled Map&#8221; and select Location as Location and for Color of saturation add &#8220;average of sentiment&#8221;. We can clearly see that people in North America and Africa are more positif feeling than people in the US for example.

[<img class="alignnone wp-image-19907 size-large" src="/wp-content/uploads/2018/11/map-1024x589.png" alt="" width="768" height="442" srcset="/wp-content/uploads/2018/11/map-1024x589.png 1024w, /wp-content/uploads/2018/11/map-300x172.png 300w, /wp-content/uploads/2018/11/map-768x442.png 768w, /wp-content/uploads/2018/11/map.png 1428w" sizes="(max-width: 768px) 100vw, 768px" />](/wp-content/uploads/2018/11/map.png)

My final result looks like this:

&nbsp;

[<img class="alignnone wp-image-19908 size-large" src="/wp-content/uploads/2018/11/dashboard-1024x577.png" alt="" width="768" height="433" srcset="/wp-content/uploads/2018/11/dashboard-1024x577.png 1024w, /wp-content/uploads/2018/11/dashboard-300x169.png 300w, /wp-content/uploads/2018/11/dashboard-768x432.png 768w, /wp-content/uploads/2018/11/dashboard.png 1483w" sizes="(max-width: 768px) 100vw, 768px" />](/wp-content/uploads/2018/11/dashboard.png)

That&#8217;s it folks! You can download my Power BI report file from [here.](https://stacor4prod.blob.core.windows.net/public/TweetSentiment.pbix)

Thanks,  
Alex