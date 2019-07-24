---
id: 13881
title: Step by Step guide on installing the Azure Usage and Billing Insights (AUBI) Portal
date: 2016-11-11T03:20:13+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://www.mscloud.be/?p=13881
permalink: /step-by-step-guide-on-installing-the-azure-usage-and-billing-insights-aubi-portal/
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
  - "6916"
  - "6916"
  - "6916"
image: /wp-content/uploads/2016/11/pb2-3-e1478794833282-150x150.png
categories:
  - Azure
  - Powershell
tags:
  - Azure
  - cubesys
  - Power BI
  - powershell
---
A lot of my customers are struggling with the billing part of Azure. They need a convenient way to review and visualize what they have consumed in Azure. I discovered the <a href="https://github.com/Microsoft/AzureUsageAndBillingPortal" target="_blank">Azure Usage and Billing Insights (AUBI) portal</a> couple of weeks ago, which does exactly this! This solution is designed to retrieve usage details of all Azure services in specific Azure subscription(s). Using a PowerBI dashboard, one can retrieve up to date billing data (Azure service usage details) of a subscription.

This blog post will cover how to install and use the AUBI portal. There are couple of steps we need to follow:

  * Download all the required files from the GitHub repository
  * First we need to create the required services in Azure
  * Next we need to deploy the Visual Studio solution to Azure Webapps
  * Then we need to configure Azure Active Directory to allow the AUBI application to be multi-tenant
  * Then we need to create the required SQL tables to store the usage information
  * And last we can start using the PowerBI desktop

# 1) Create required services in Azure

To be able to run the Azure Usage and Billing Insights Portal you will need the following services in Azure:

  * One public **website** called Registration where any user can provide access to the site and register their Azure subscriptions.
  * One **website** called Dashboard, where only authenticated users can see the list of registered subscriptions and trigger a job to re-generate up to date billing data in case of any inconsistency.
  * One **AzureSQL Server** to hold billing and usage data for all registered subscriptions.
  * One **Azure Storage Queue** to hold “generate data” requests.
  * One schedule base (every UTC night) running **webjob** that is triggered once a day to create “generate data” request for each registered subscription.
  * One continuous running **webjob** to process requests that are waiting in the Azure Storage Queue.
  * **PowerBi** dashboard for data visualization of all or per subscription Azure service billing and usage details like service unit, quantity, usage duration, etc.

To create the services, you have to run the following script in PowerShell: **CreateAzureServicesScript.ps1** with its dependency file **CreateAzureServicesScriptResources.json**

First open the JSON template file and change the variables if required. Make sure to change the subscription name and default password to reflect your own subscription. Don&#8217;t change the region though, as the ARM template is using some Application Insights components which are only available in Central US region.

Next, open PowerShell ISE in administrative mode and run the .\CreateAzureServicesScript.ps1 script

<img class="alignnone size-full wp-image-13531" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image.png" alt="image.png" width="1024" height="501" srcset="/wp-content/uploads/2016/10/image.png 1024w, /wp-content/uploads/2016/10/image-300x147.png 300w, /wp-content/uploads/2016/10/image-768x376.png 768w, /wp-content/uploads/2016/10/image-330x160.png 330w" sizes="(max-width: 1024px) 100vw, 1024px" /> 

You can verify if the Azure services have been created successfully in the Azure portal

<img class="alignnone size-full wp-image-13541" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image1.png" alt="image1.png" width="1024" height="532" srcset="/wp-content/uploads/2016/10/image1.png 1024w, /wp-content/uploads/2016/10/image1-300x156.png 300w, /wp-content/uploads/2016/10/image1-768x399.png 768w" sizes="(max-width: 1024px) 100vw, 1024px" /> 

Make sure your client IP address has been added to the SQL server firewall exception list, or you will run into issues when trying to deploy the solution with Visual Studio later on.

Once the script is successfully executed, it will output all parameter values with their names in PowerShell ISE.

Don&#8217;t close your PowerShell window as we will need those output parameters later on to update the configuration (Web.config and App.config) files inside the solution with these new service settings before compiling and publishing them with Visual Studio.

<img class="alignnone size-full wp-image-13561" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/AUBI11.png" alt="AUBI11.png" width="757" height="768" srcset="/wp-content/uploads/2016/10/AUBI11.png 757w, /wp-content/uploads/2016/10/AUBI11-296x300.png 296w, /wp-content/uploads/2016/10/AUBI11-55x55.png 55w" sizes="(max-width: 757px) 100vw, 757px" /> 

In case there are any errors during the execution of the Powershell script (maybe because the service name that you assigned in the parameters is not unique), you can delete the resource group from Azure management portal and restart the Powershell script with new parameters.

# 2) Deploy the AUBI Solution with Visual Studio

Using the output values from the PowerShell script we can now update our web.config files and App.config files. Open the **AUI.sln** in Visual Studio. Next open the **Web.config** file and **App.config** file under Registration, Dashboard, WebJobUsageDaily and WebJobBillingData and enter your values from the PowerShell script

<img class="alignnone size-full wp-image-13581" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image2.png" alt="image2.png" width="1024" height="376" srcset="/wp-content/uploads/2016/10/image2.png 1024w, /wp-content/uploads/2016/10/image2-300x110.png 300w, /wp-content/uploads/2016/10/image2-768x282.png 768w" sizes="(max-width: 1024px) 100vw, 1024px" /> 

After all these configuration updates, compile and publish the projects and Web jobs on Azure. Right click the project and click **build solution**:

<img class="alignnone size-full wp-image-13601" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image3.png" alt="image3.png" width="870" height="768" srcset="/wp-content/uploads/2016/10/image3.png 870w, /wp-content/uploads/2016/10/image3-300x265.png 300w, /wp-content/uploads/2016/10/image3-768x678.png 768w" sizes="(max-width: 870px) 100vw, 870px" /> 

After the build is completed, click **publish**

<img class="alignnone size-full wp-image-13621" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image4.png" alt="image4.png" width="439" height="768" srcset="/wp-content/uploads/2016/10/image4.png 439w, /wp-content/uploads/2016/10/image4-171x300.png 171w" sizes="(max-width: 439px) 100vw, 439px" /> 

Select Microsoft Azure Web Apps

<img class="alignnone size-full wp-image-13641" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image5.png" alt="image5.png" width="967" height="768" srcset="/wp-content/uploads/2016/10/image5.png 967w, /wp-content/uploads/2016/10/image5-300x238.png 300w, /wp-content/uploads/2016/10/image5-768x610.png 768w" sizes="(max-width: 967px) 100vw, 967px" /> 

Select your Azure subscription and select the AUI dashboard first

<img class="alignnone size-full wp-image-13661" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image6.png" alt="image6.png" width="837" height="768" srcset="/wp-content/uploads/2016/10/image6.png 837w, /wp-content/uploads/2016/10/image6-300x275.png 300w, /wp-content/uploads/2016/10/image6-768x705.png 768w" sizes="(max-width: 837px) 100vw, 837px" /> 

configure your Webapp as below

<img class="alignnone size-full wp-image-13681" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image7.png" alt="image7.png" width="966" height="768" srcset="/wp-content/uploads/2016/10/image7.png 966w, /wp-content/uploads/2016/10/image7-300x239.png 300w, /wp-content/uploads/2016/10/image7-768x611.png 768w" sizes="(max-width: 966px) 100vw, 966px" /> 

<img class="alignnone size-full wp-image-13701" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image8.png" alt="image8.png" width="972" height="768" srcset="/wp-content/uploads/2016/10/image8.png 972w, /wp-content/uploads/2016/10/image8-300x237.png 300w, /wp-content/uploads/2016/10/image8-768x607.png 768w" sizes="(max-width: 972px) 100vw, 972px" /> 

Same for the registration portal that we need to publish as well.

You have to enter the authentication Active Directory (AD), so only the users defined under this AD will be able to access the Dashboard webpage.

<img class="alignnone size-full wp-image-13711" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image9.png" alt="image9.png" width="954" height="768" srcset="/wp-content/uploads/2016/10/image9.png 954w, /wp-content/uploads/2016/10/image9-300x242.png 300w, /wp-content/uploads/2016/10/image9-768x618.png 768w" sizes="(max-width: 954px) 100vw, 954px" /> 

And lasty we also need to publish the Azure Webjobs

<img class="alignnone size-full wp-image-13731" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image10.png" alt="image10.png" width="381" height="768" srcset="/wp-content/uploads/2016/10/image10.png 381w, /wp-content/uploads/2016/10/image10-149x300.png 149w" sizes="(max-width: 381px) 100vw, 381px" /> 

<img class="alignnone size-full wp-image-13751" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image11.png" alt="image11.png" width="973" height="768" srcset="/wp-content/uploads/2016/10/image11.png 973w, /wp-content/uploads/2016/10/image11-300x237.png 300w, /wp-content/uploads/2016/10/image11-768x606.png 768w" sizes="(max-width: 973px) 100vw, 973px" /> 

# 3) Configure Azure Active Directory

We still need to change some settings in Azure AD to make our application multi-tenant. You can open the default Active Directory service settings in the old portal (it is not supported in the new Azure portal at the time of writing this guide) to finalize its settings. Click on the app name, and open the applications configure page. In the configuration settings of the AD app, apply the following changes in order

  * Change “APP ID URI” value to an any valid URI in your directory.  
    i.e.: [http://cubesys.onmicrosoft.com/auiv4](http://fabrikam.onmicrosoft.com/auiv4)  
    As in the above sample, your directory name (i.e. cubesys.onmicrosoft.com) can be found under the settings page in the old portal.

<img class="alignnone size-full wp-image-13771" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image12.png" alt="image12.png" width="941" height="249" srcset="/wp-content/uploads/2016/10/image12.png 941w, /wp-content/uploads/2016/10/image12-300x79.png 300w, /wp-content/uploads/2016/10/image12-768x203.png 768w" sizes="(max-width: 941px) 100vw, 941px" /> 

Change the “Permissions to other applications” property by adding “Windows Azure Service Management API” value to the list. _Add “Windows Azure Service Management API” to the list. Then change its “Delegated Permission” property to 1, as shown in the below picture.  __Change its “Delegated Permission” value to 1. _Also in the same settings page, be sure that “Windows Azure Active Directory” is selected with “Sign in and read user profile” delegated permission as shown in the below picture

<img class="alignnone size-full wp-image-13782" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image13.png" alt="image13.png" width="931" height="387" srcset="/wp-content/uploads/2016/10/image13.png 931w, /wp-content/uploads/2016/10/image13-300x125.png 300w, /wp-content/uploads/2016/10/image13-768x319.png 768w" sizes="(max-width: 931px) 100vw, 931px" /> 

<img class="alignnone size-full wp-image-13801" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image14.png" alt="image14.png" width="1024" height="227" srcset="/wp-content/uploads/2016/10/image14.png 1024w, /wp-content/uploads/2016/10/image14-300x67.png 300w, /wp-content/uploads/2016/10/image14-768x170.png 768w" sizes="(max-width: 1024px) 100vw, 1024px" /> 

# 4) Create the SQL Tables

Before being able to collect usage data you need to connect to the newly created SQL server with Visual Studio, SQL Management Studio and **run** the TSQL commands in &#8220;**SQLScripts.sql**&#8221; file to create a table to store billing data and its dependent StoredProcedure. You can find the SQLSCRIPT.SQL file on the right hand side in VisualStudio

<img class="alignnone size-full wp-image-13821" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image15.png" alt="image15.png" width="1024" height="151" srcset="/wp-content/uploads/2016/10/image15.png 1024w, /wp-content/uploads/2016/10/image15-300x44.png 300w, /wp-content/uploads/2016/10/image15-768x113.png 768w" sizes="(max-width: 1024px) 100vw, 1024px" /> 

<img class="alignnone size-full wp-image-13841" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image16.png" alt="image16.png" width="430" height="600" srcset="/wp-content/uploads/2016/10/image16.png 430w, /wp-content/uploads/2016/10/image16-215x300.png 215w" sizes="(max-width: 430px) 100vw, 430px" /> 

Click Run in the right top corner

<img class="alignnone size-full wp-image-13861" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/10/image17.png" alt="image17.png" width="826" height="733" srcset="/wp-content/uploads/2016/10/image17.png 826w, /wp-content/uploads/2016/10/image17-300x266.png 300w, /wp-content/uploads/2016/10/image17-768x682.png 768w" sizes="(max-width: 826px) 100vw, 826px" /> 

#  5) Registration of subscriptions

Once you install and complete all the required configuration steps anyone can access the registration website and register their Azure subscription for monitoring.

  1. Open a browser InPrivate browsing or logout from all your prev. sessions
  2. Go to the URL address of the Registration website to register your Azure subscription.
  3. Logon using your Azure credentials
  4. In the final step a list of your azure subscriptions will be listed. Each list item has a subscription name, a textbox and “Allow Monitoring” button. The user is expected to enter a display name for each subscription (i.e. first and last names) that will be shown in the reports.
  5. Click allow monitoring

<img class="alignnone size-full wp-image-16251" src="http://www.mscloud.be/wp-content/uploads/2016/11/2016-11-10_9-06-33-1.png" alt="2016-11-10_9-06-33" width="1819" height="690" srcset="/wp-content/uploads/2016/11/2016-11-10_9-06-33-1.png 1819w, /wp-content/uploads/2016/11/2016-11-10_9-06-33-1-300x114.png 300w, /wp-content/uploads/2016/11/2016-11-10_9-06-33-1-768x291.png 768w, /wp-content/uploads/2016/11/2016-11-10_9-06-33-1-1024x388.png 1024w" sizes="(max-width: 1819px) 100vw, 1819px" /> 

# 6) Power Bi Desktop

You need to download and install the PowerBI desktop application from <https://powerbi.microsoft.com/en-us/desktop>. Once you have it, you can open the **AUIDashboard.pbix** file to modify the existing report and publish it to PowerBI online.

When you open the AUIDashboard.pbix file, initially you will see many errors like &#8220;Fix This&#8221; as there is no data, because no data connection set.

<img class="alignnone size-full wp-image-15962" src="http://www.mscloud.be/wp-content/uploads/2016/11/img22.png" alt="img22.png" width="600" height="391" srcset="/wp-content/uploads/2016/11/img22.png 600w, /wp-content/uploads/2016/11/img22-300x196.png 300w" sizes="(max-width: 600px) 100vw, 600px" /> 

  1. In the PowerBI Desktop, click **Edit Queries** button
  2. In the new window, click “**Data Source Settings**” to make required Database name, SQL Server password updates, etc.

<img class="alignnone size-full wp-image-16291" src="http://www.mscloud.be/wp-content/uploads/2016/11/permission.png" alt="permission" width="713" height="285" srcset="/wp-content/uploads/2016/11/permission.png 713w, /wp-content/uploads/2016/11/permission-300x120.png 300w" sizes="(max-width: 713px) 100vw, 713px" /> 

Finally after the permissions have been set correctly in Power BI the data will start to appear:

<img class="alignnone size-full wp-image-16381" src="http://www.mscloud.be/wp-content/uploads/2016/11/pb1-3.png" alt="pb1" width="2097" height="1278" srcset="/wp-content/uploads/2016/11/pb1-3.png 2097w, /wp-content/uploads/2016/11/pb1-3-300x183.png 300w, /wp-content/uploads/2016/11/pb1-3-768x468.png 768w, /wp-content/uploads/2016/11/pb1-3-1024x624.png 1024w" sizes="(max-width: 2097px) 100vw, 2097px" /> 

<img class="alignnone size-full wp-image-16401" src="http://www.mscloud.be/wp-content/uploads/2016/11/pb2.png" alt="pb2" width="2097" height="1278" srcset="/wp-content/uploads/2016/11/pb2.png 2097w, /wp-content/uploads/2016/11/pb2-300x183.png 300w, /wp-content/uploads/2016/11/pb2-768x468.png 768w, /wp-content/uploads/2016/11/pb2-1024x624.png 1024w" sizes="(max-width: 2097px) 100vw, 2097px" /> 

# Conclusion

As you can see it&#8217;s relatively easy to deploy the Azure Usage and Billing Portal to visualize your Azure bill.

I suggest you look at this [video](https://channel9.msdn.com/blogs/Mustafa-Kasap/How-to-Setup-the-Azure-Usage--Billing-Portal) from Chris and Mustafa on how to setup the Azure billing Portal.

If you have any questions, please let me know.

Kind regards,

Alexandre Verkinderen