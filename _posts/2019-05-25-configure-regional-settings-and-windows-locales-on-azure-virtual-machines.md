---
id: 19986
title: Configure regional settings on Azure Virtual Machines
date: 2019-05-25T13:28:08+10:00
author: alexandre@verkinderen.com
guid: http://mscloud.be/?p=19986
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
  - "304"
categories:
  - Azure
  - Powershell
tags:
  - Azure
  - powershell
  - Virtual Machines
---
By default every Windows virtual machine that you deploy in Azure from the marketplace will be deployed using US regional settings. So the timezone, time format, currency, keyboard will all be in EN-US.  
I got a few requests lately from customers and others if it would be possible to automate the regional settings, sytem locales and input locales configuration. This blogpost will cover how to create an XML settings file that contains all of our regional settings and how to apply those regional settings to our Virtual Machines in Azure. To be able to achieve this we are going to need 2 things: an XML file containing our regional settings and a PowerShell script to apply the regional settings.

## Regional Settings File

We are basically going to use an XML file, like we would back in the old days, to do unattended Windows installations. You can find an example for Australia here:

<https://github.com/averkinderen/Azure/blob/master/101-ServerBuild/AURegion.xml>  
  
Syntax:

* Userlist: This setting specifies the user account for which we need to do the change settings. CopySettingsToDefaultUserAcct and CopySettingsToSystemAcct are the parameters that can be used to copy the settings to all users and also the system account(logonUI screen).
  * SystemLocale: This is for programs that do not use Unicode. (Probably not needed anymore. )
  * InputPreferences: This is for keyboard layout settings. For a list of Input Locales have a look [here](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/default-input-locales-for-windows-language-packs).
  * GeoID/Location Preferences: current location field under the location tab. For a list of GeoID/locations have a look [here](https://docs.microsoft.com/en-us/windows/desktop/intl/table-of-geographical-locations).
  * UserLocale: These are the settings for the currency, number formatting and date formatting. So if you don&#8217;t want month/day/year (this doesn&#8217;t make sense at all to me, but anyway 😉 )but would like day/month/year instead change this setting.

Modify the XML to your own needs and put it on a Storage Account or on github.

## PowerShell Script

Next, we will create a PowerShell script to apply the regional settings. The script will first download the XML file created above and then apply the XML file with the regional settings control panel applet. You can find the PowerShell script here:

https://raw.githubusercontent.com/averkinderen/Azure/master/101-ServerBuild/serverbuild.ps1

## Applying the PowerShell script with the CustomScriptExtension

You could call the PowerShell script from your ARM template as described here <https://docs.microsoft.com/en-us/azure/virtual-machines/extensions/custom-script-windows> . For now, I will just deploy the CustomScriptExtension from the portal to show the regional settings. Click on **Extensions** and **Add** to add a new extension

<figure class="wp-block-image">
<img src="http://mscloud.be/wp-content/uploads/2019/05/image-2.png"/>
</figure>

Scroll down to the **Custom Script Extension** and click **Create.** Select the ServerBuild.ps1 Script and click **OK.**
<figure class="wp-block-image">
<img src="http://mscloud.be/wp-content/uploads/2019/05/image-3-1024x175.png"/>
</figure>

## Result

Let&#8217;s verify now if the regional settings have been applied correctly. Look in the Evenviewer and see if you can find Event 13000
<figure class="wp-block-image">
<img src="http://mscloud.be/wp-content/uploads/2019/05/image-1024x524.png"/>
</figure>

## Conclusion

As you can see it&#8217;s relatively easy to change the regional settings and configuration of your virtual machines deployed in Azure using market place images.  
I hear a lot of customers telling me they create their own customized images with all the settings like regional settings, firewall, monitoring agents and others embedded in the image. **My recommendation is to avoid this as much as you can.** Just like we are switching from traditional infrastructure deployment models to Infrastructure as Code, we should also switch to Configuration as Code.

Hope this helps,

Alexandre
