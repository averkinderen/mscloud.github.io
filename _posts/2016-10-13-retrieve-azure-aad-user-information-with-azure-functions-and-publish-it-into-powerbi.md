---
id: 13921
title: Retrieve Azure AAD user information with Azure Functions and publish it into PowerBI
date: 2016-10-13T22:35:45+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=13921
permalink: /retrieve-azure-aad-user-information-with-azure-functions-and-publish-it-into-powerbi/
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
  - "13676"
  - "13676"
categories:
  - Azure
  - Powershell
tags:
  - Azure
  - Azure Functions
  - cubesys
  - Power BI
  - powershell
---
Few days ago I had a requirement to retrieve user information from Azure Active Directory and publish the data into a Power BI dashboard.

In PowerBI you can&#8217;t directly query Azure Active Directory (there is, however, a [connector](https://powerbi.microsoft.com/en-us/integrations/active-directory/) to query an on premise Active Directory environment) so I had a quick chat with my good friend and CDM MVP [Tao Yang](https://twitter.com/MrTaoYang) about how this could be achieved. After a few brainstorm sessions he suggested to try [Azure Functions](https://azure.microsoft.com/en-us/services/functions/) to retrieve the user information from Azure AAD.

**In this blog post I will show you how to build an Azure Function to connect to Azure AAD and publish the data to PowerBI**. Tao has written [another blogpost](http://blog.tyang.org/2016/10/14/feeding-your-power-bi-reports-from-azure-functions) about how to retrieve information from Azure VMs and use that in Power BI, so make sure to have a look at his blogpost as well.

## Requirements

You will need to following components:

  * Azure Subscription
  * Azure Function (which we are going to build in this blogpost)
  * MSOnline PowerShell Module (to connect and retrieve the Azure AAD users)
  * [Power BI online account](https://powerbi.microsoft.com/en-us/features/)
  * [Power BI desktop](https://powerbi.microsoft.com/en-us/desktop/)

# Build new Azure Functions to retrieve Azure AAD information

In the Azure portal **create a new** Azure Function app and give it a **name**. Make sure to select **Dynamic** as the App Service Plan so you only pay for what you consume.

[<img class="alignnone size-medium wp-image-14071" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/newfunctionapp-185x300.png" alt="newfunctionapp" width="185" height="300" srcset="/wp-content/uploads/2016/10/newfunctionapp-185x300.png 185w, /wp-content/uploads/2016/10/newfunctionapp.png 371w" sizes="(max-width: 185px) 100vw, 185px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/newfunctionapp.png)

You will find your new Azure Function in **App services** after the deployment has completed.

[<img class="alignnone size-large wp-image-14091" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/newfunctions-1024x503.png" alt="newfunctions" width="768" height="377" srcset="/wp-content/uploads/2016/10/newfunctions-1024x503.png 1024w, /wp-content/uploads/2016/10/newfunctions-300x147.png 300w, /wp-content/uploads/2016/10/newfunctions-768x377.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/newfunctions.png)

&nbsp;

## Upload the MSonline PowerShell Module in Azure Functions

To be able to read the Active Directory user data from Azure AAD you will need the MSOnline PowerShell module installed into your Azure Function. Firstly you will need to download the MSOnline PowerShell module locally to your computer and then upload it your Azure Function.

<pre class="lang:ps decode:true ">save-module msonline -repository PSGallery -Path "C:\temp"</pre>

Once you have the module you need to upload it to Azure Functions.  I&#8217;m not going to cover how to import customer PowerShell modules into Azure functions in this post as [Tao has already covered](http://blog.tyang.org/2016/10/07/using-custom-powershell-modules-in-azure-functions/) that. Make sure to follow Tao&#8217;s blog or your Azure function will fail.

Now you are ready to start using your first Azure Function!

## Configure your Azure Function

To be able to authenticate against our Azure AAD environment we will need to provide some credentials. I&#8217;m not going to describe in this blogpost how to handle secrets in Azure functions as [Tao Yang](http://blog.tyang.org/2016/10/08/securing-passwords-in-azure-functions/) and [David O&#8217;brien](https://david-obrien.net/2016/09/azure-functions-secrets/) have already covered how to do that.

Click on **Configure App Settings** and change the following settings:

  * Change the platform from 32-bit to **64-bit**
  * Add a new App Setting called **Password** with the encrypted password of our Office 365 user. We will retrieve this custom app setting later on in our PowerShell script
  * Add a new App Setting called **User **with the username of our Office 365 user. We will retrieve this custom app setting later on in our PowerShell script

[<img class="alignnone size-large wp-image-14092" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/configurefunction11-1024x785.png" alt="configurefunction1" width="768" height="589" srcset="/wp-content/uploads/2016/10/configurefunction11-1024x785.png 1024w, /wp-content/uploads/2016/10/configurefunction11-300x230.png 300w, /wp-content/uploads/2016/10/configurefunction11-768x588.png 768w, /wp-content/uploads/2016/10/configurefunction11-240x185.png 240w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/configurefunction11.png)

Click on **Save.**

## Create a new Azure function

Select **New Function**, change the language to **PowerShell** and select **Empty &#8211; ****PowerShell**. Give it a name and click **Create**

[<img class="alignnone wp-image-13991 size-large" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/newfunction-1024x554.png" alt="newfunction" width="768" height="416" srcset="/wp-content/uploads/2016/10/newfunction-1024x554.png 1024w, /wp-content/uploads/2016/10/newfunction-300x162.png 300w, /wp-content/uploads/2016/10/newfunction-768x415.png 768w, /wp-content/uploads/2016/10/newfunction.png 1098w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/newfunction.png)

Now that we have our Azure Function up and running and configured we need to retrieve the Azure AD data. The following PowerShell script will connect to you Azure AAD environment with the provided credentials and retrieve Azure AD user information.

Copy the following code into your function:

<pre class="lang:ps decode:true">$FunctionName = 'GetAADUsers'
$MaxResults = 2000
$ModuleName = 'MSOnline'
$ModuleVersion = '1.0'
$username = $Env:User
$pw = $Env:Password
#import PS module
$PSModulePath = "D:\home\site\wwwroot\$FunctionName\bin\$ModuleName\$ModuleVersion\$ModuleName.psd1"
Import-module $PSModulePath

#credential
$keypath = "D:\home\site\wwwroot\$FunctionName\bin\keys\PassEncryptKey.key"
$secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
$credential = New-Object System.Management.Automation.PSCredential ($username, $secpassword)

Connect-MsolService -Credential $credential

$users = Get-MsolUser -MaxResults $MaxResults
$HTMLOutput = ($users | ConvertTo-Html -Title 'Azure AD Users' -Property DisplayName, FirstName, LastName, UserPrincipalName, LastPasswordChangeTimestamp, PhoneNumber, StreetAddress, City, State, Country, PostalCode, PasswordNeverExpires, IsLicensed) | out-string
Out-file -encoding Ascii -FilePath $res -InputObject $HTMLOutput</pre>

And, as you can see in the script above we are using the app settings we have created earlier as variables (<span class="lang:ps decode:true crayon-inline ">$Env:User and $Env:Password</span>)in our script.

[<img class="alignnone wp-image-14411 size-large" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/psfunction1-1024x603.png" alt="psfunction" width="768" height="452" srcset="/wp-content/uploads/2016/10/psfunction1-1024x603.png 1024w, /wp-content/uploads/2016/10/psfunction1-300x177.png 300w, /wp-content/uploads/2016/10/psfunction1-768x452.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/psfunction1.png)

We are now ready to test our Azure function. Copy the function URL at the top of the page and open PowerShell ISE.

## Test GetAzureAAD function

To test and verify if the Azure function is working we just open PowerShell ISE and call our function URI:

[<img class="alignleft wp-image-13951 size-large" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/callfunction-1024x16.png" alt="callfunction" width="768" height="12" srcset="/wp-content/uploads/2016/10/callfunction-1024x16.png 1024w, /wp-content/uploads/2016/10/callfunction-300x5.png 300w, /wp-content/uploads/2016/10/callfunction-768x12.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/callfunction.png)

# 

After this we can verify our call was successful by viewing the content of our request:

<pre class="lang:ps decode:true ">$request.content</pre>

[<img class="alignnone wp-image-13971 size-large" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/functionuser-1024x226.png" alt="functionuser" width="768" height="170" srcset="/wp-content/uploads/2016/10/functionuser-1024x226.png 1024w, /wp-content/uploads/2016/10/functionuser-300x66.png 300w, /wp-content/uploads/2016/10/functionuser-768x169.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/functionuser.png)

In your favourite browser it will look like this:

[<img class="alignnone size-large wp-image-14451" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/ugly-1024x208.png" alt="ugly" width="768" height="156" srcset="/wp-content/uploads/2016/10/ugly-1024x208.png 1024w, /wp-content/uploads/2016/10/ugly-300x61.png 300w, /wp-content/uploads/2016/10/ugly-768x156.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/ugly.png)

You can check for any errors or monitor the runtime of your Azure Function by clicking monitor in the Azure Portal.

[<img class="alignnone wp-image-14061 size-large" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/monitor-1024x321.png" alt="monitor" width="768" height="241" srcset="/wp-content/uploads/2016/10/monitor-1024x321.png 1024w, /wp-content/uploads/2016/10/monitor-300x94.png 300w, /wp-content/uploads/2016/10/monitor-768x241.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/monitor.png)

As I discovered later on, you cannot use the output that we generate in our Azure Function in Power BI online. You can however use it in Power BI desktop, but not in Power BI online as you are unable to refresh the data and define a schedule refresh. This is because the content type of the output is not set correctly. I believe this is a PowerShell limitation in Azure Function (it&#8217;s still in preview) and a bug in Power BI. So Tao came to the rescue again and created another Azure Function in C# to wrap our PowerShell function and generate a proper output. You can read more about this on [Tao&#8217;s blog](http://blog.tyang.org/2016/10/13/making-powershell-based-azure-functions-to-produce-html-outputs/).

Select **New Function**, change the language to **C#** and select **HttpTrigger-C#**. Give it a name and click **Create**

[<img class="alignnone size-large wp-image-14431" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/createc-1024x374.png" alt="createc" width="768" height="281" srcset="/wp-content/uploads/2016/10/createc-1024x374.png 1024w, /wp-content/uploads/2016/10/createc-300x109.png 300w, /wp-content/uploads/2016/10/createc-768x280.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/createc.png)

In your function replace the existing code with the following code from [Tao](https://gist.github.com/tyconsulting/eae44357f14818006bf0ba94bf07bae1):



As you can see we are creating a C# wrapper that need a requesturl (which is our URI from our first function). Click on **Save**

[<img class="alignnone size-large wp-image-14441" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/triggerget-1024x368.png" alt="triggerget" width="768" height="276" srcset="/wp-content/uploads/2016/10/triggerget-1024x368.png 1024w, /wp-content/uploads/2016/10/triggerget-300x108.png 300w, /wp-content/uploads/2016/10/triggerget-768x276.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/triggerget.png)

Now open your browser and copy paste the url from the C# Azure function and append the parameter requesturl behind the URI with the URI of the first Azure Function. So this HTTPTriggerProxy function calls the other url that you specified.

[<img class="alignnone size-large wp-image-14461" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/url-1024x17.png" alt="url" width="768" height="13" srcset="/wp-content/uploads/2016/10/url-1024x17.png 1024w, /wp-content/uploads/2016/10/url-300x5.png 300w, /wp-content/uploads/2016/10/url-768x12.png 768w, /wp-content/uploads/2016/10/url.png 1475w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/url.png)

The output looks a lot nice now:

[<img class="alignnone size-large wp-image-14471" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/good-1024x297.png" alt="good" width="768" height="223" srcset="/wp-content/uploads/2016/10/good-1024x297.png 1024w, /wp-content/uploads/2016/10/good-300x87.png 300w, /wp-content/uploads/2016/10/good-768x223.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/good.png)

Now that we have our data that we want we can retrieve that data and use it in Power BI.

# Retrieve Azure function data into Power BI

To retrieve the data from our Azure Function in PowerBI, click on **Get Data** in Power BI desktop and select **Web**

[<img class="alignnone size-full wp-image-14201" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/getdata.png" alt="getdata" width="206" height="466" srcset="/wp-content/uploads/2016/10/getdata.png 206w, /wp-content/uploads/2016/10/getdata-133x300.png 133w" sizes="(max-width: 206px) 100vw, 206px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/getdata.png)

In the next window provide the **function URL** you copied earlier. The **basic** option is enough for the purpose of this demo, in the advanced mode you can define HTTP request headers and command timeouts which we don&#8217;t need now.

[<img class="alignnone size-medium wp-image-14211" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/getweb-300x108.png" alt="getweb" width="300" height="108" srcset="/wp-content/uploads/2016/10/getweb-300x108.png 300w, /wp-content/uploads/2016/10/getweb.png 697w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/getweb.png)

Select **Table 0** in the next window and click **Load**. You will now be able to use the data from your Azure function in Power BI. Below you can see a quick example of my AD dashboard that gives me a quick overview of unlicensed users, location of the users, etc. I&#8217;m not going to go into detail on the different Power BI visuals, but below you can find an example of my Azure AD Power BI dashboard.

[<img class="size-large wp-image-14191 alignnone" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/powerbi-1024x605.png" alt="powerbi" width="768" height="454" srcset="/wp-content/uploads/2016/10/powerbi-1024x605.png 1024w, /wp-content/uploads/2016/10/powerbi-300x177.png 300w, /wp-content/uploads/2016/10/powerbi-768x453.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/powerbi.png)

That&#8217;s it! How awesome is this? Let&#8217;s publish our dashboard now to Power BI online.

# Publish dashboard to Power BI online

Once you are done creating your Power BI dashboard you can publish it to Power BI online and share it with others. In Power BI desktop, click **Publish**

[<img class="alignnone size-medium wp-image-14381" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/publish-300x44.png" alt="publish" width="300" height="44" srcset="/wp-content/uploads/2016/10/publish-300x44.png 300w, /wp-content/uploads/2016/10/publish-768x114.png 768w, /wp-content/uploads/2016/10/publish-1024x152.png 1024w, /wp-content/uploads/2016/10/publish.png 1426w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/publish.png)

Once published select **Open** in Power BI

<img class="alignnone size-medium wp-image-14371" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/publish1-300x131.png" alt="publish1" width="300" height="131" srcset="/wp-content/uploads/2016/10/publish1-300x131.png 300w, /wp-content/uploads/2016/10/publish1.png 744w" sizes="(max-width: 300px) 100vw, 300px" /> 

To refresh the data automatically click on your new **Dataset** and select **Schedule Refresh**

[<img class="alignnone size-medium wp-image-14341" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/dataset-200x300.png" alt="dataset" width="200" height="300" srcset="/wp-content/uploads/2016/10/dataset-200x300.png 200w, /wp-content/uploads/2016/10/dataset-768x1150.png 768w, /wp-content/uploads/2016/10/dataset-684x1024.png 684w, /wp-content/uploads/2016/10/dataset.png 818w" sizes="(max-width: 200px) 100vw, 200px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/dataset.png)

Configure your dataset as seen below:

[<img class="alignnone size-medium wp-image-14361" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/dataset1-300x241.png" alt="dataset1" width="300" height="241" srcset="/wp-content/uploads/2016/10/dataset1-300x241.png 300w, /wp-content/uploads/2016/10/dataset1-768x618.png 768w, /wp-content/uploads/2016/10/dataset1-1024x824.png 1024w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/dataset1.png)

click on edit credentials and make sure the authentication method is set to **Anonymous**

[<img class="alignnone size-medium wp-image-14351" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/datasetauth-300x164.png" alt="datasetauth" width="300" height="164" srcset="/wp-content/uploads/2016/10/datasetauth-300x164.png 300w, /wp-content/uploads/2016/10/datasetauth.png 665w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/datasetauth.png)

# Conclusion

Using Azure Functions to retrieve data enables a whole new world of capabilities to retrieve and pull data into PowerBI from data sources that are not natively supported by PowerBI!

Are you missing any data sources in Power BI today? What data sources would you like to query that is not natively supported by Power BI?

Thank you,

Alexandre
