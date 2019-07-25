---
id: 13151
title: Add a custom image to Azure Stack
date: 2016-09-15T01:21:19+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=13151
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
  - "3526"
  - "3526"
  - "3526"
categories:
  - Azure
  - MAS
tags:
  - azure stack
  - cubesys
  - powershell
---
In this blog post I will explain how you can add multiple custom images to Azure Stack.

At <a href="http://www.cubesys.com.au" target="_blank">cubesys</a> we have a brand new Azure Stack environment that we use as a demo and test environment for our consultants. Each consultant has his own subscription with pre-defined quotas that they can use to build, test and destroy whenever and whatever they want to test. One of our senior consultants asked me to add the following custom images as he wanted to test and validate a System Center upgrade scenario:

  * Windows 7 SP1 x64 Enterprise
  * Windows 8.1 x64 Enterprise
  * Windows 10 (Build 1511) x64 Enterprise
  * Windows Server 2008 R2 SP1 Datacenter
  * Windows Server 2012 Datacenter

So let’s make our tenant happy shall we?

# Sysprep the virtual machines

Initially you will have to sysprep the virtual machines.

  1. Create a new virtual machine in Hyper-V 
      1. make sure it’s <span style="text-decoration: underline;"><strong>generation 1</strong></span>
      2. and the hard drive needs to be <u><strong>VHD</strong> </u>and not **VHDX**
  2. Install the operating system

[<img class="alignnone size-medium wp-image-13041" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/SNAGHTMLd020970-300x41.png" alt="SNAGHTMLd020970.png" width="300" height="41" srcset="/wp-content/uploads/2016/09/SNAGHTMLd020970-300x41.png 300w, /wp-content/uploads/2016/09/SNAGHTMLd020970-768x104.png 768w, /wp-content/uploads/2016/09/SNAGHTMLd020970.png 1024w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/SNAGHTMLd020970.png)

&nbsp;

  1. Once the operating system is installed you need to sysprep the machine using the following command 
      1. For Windows 8 and after: 
          1. open a Command Prompt window as an administrator, and then move to the **%WINDIR%\system32\sysprep** directory.
          2. Run the following command: 
            [php]Sysprep /generalize /shutdown  /oobe /mode:vm[/php]
    
      2. Anything before Windows 8 
          1. open a Command Prompt window as an administrator, and then move to the **%WINDIR%\system32\sysprep** directory
          2. Run the following command: 
            [php] Sysprep /generalize /shutdown /oobe [/php]

[<img class="alignnone size-medium wp-image-13061" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/sysprep-300x186.jpg" alt="sysprep.jpg" width="300" height="186" srcset="/wp-content/uploads/2016/09/sysprep-300x186.jpg 300w, /wp-content/uploads/2016/09/sysprep-768x476.jpg 768w, /wp-content/uploads/2016/09/sysprep.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/sysprep.jpg)

Once complete the virtual machines will shutdown automatically. Copy the sysprepped virtual hard drives to another location. In my case E:\templates

[<img class="alignnone size-medium wp-image-13081" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image11-300x60.png" alt="image11.png" width="300" height="60" srcset="/wp-content/uploads/2016/09/image11-300x60.png 300w, /wp-content/uploads/2016/09/image11-768x155.png 768w, /wp-content/uploads/2016/09/image11.png 1024w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image11.png)

&nbsp;

# Add the image to the Platform Image Repository

Once we have all our virtual machines sysprepped and have copied the virtual hard drives we can add them to Azure Stack. To add a new image to Azure stack it needs to be added to the Platform Image Repository or PIR. Microsoft has provided a PowerShell script (CopyImageToPlatformImageRepository.ps1) to do this.

You can find this PowerShell script on the MicrosoftAzureStackPOC.vhd virtual hard drive.

  * Right click on the vhd file and mount the VHD
  * Get the Drive letter of the DATAIMAGE drive

[<img class="alignnone size-medium wp-image-13101" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/azurestackpir-300x119.png" alt="azurestackpir.png" width="300" height="119" srcset="/wp-content/uploads/2016/09/azurestackpir-300x119.png 300w, /wp-content/uploads/2016/09/azurestackpir-768x305.png 768w, /wp-content/uploads/2016/09/azurestackpir-770x309.png 770w, /wp-content/uploads/2016/09/azurestackpir.png 778w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/azurestackpir.png)

&nbsp;

  * Use PowerShell and Navigate to D:\CRP\VM\Microsoft.AzureStack.Compute.Installer\content\Scripts where you will find the CopyImageToPlatformImageRepository.ps1 PowerShell script

[<img class="alignnone size-medium wp-image-13112" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image12-300x101.png" alt="image12.png" width="300" height="101" srcset="/wp-content/uploads/2016/09/image12-300x101.png 300w, /wp-content/uploads/2016/09/image12-768x259.png 768w, /wp-content/uploads/2016/09/image12.png 972w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image12.png)

The script requires the following parameters:

  1. For **PlatformImageRepositoryPath**, type `<a href="file://\\SOFS\Share\CRP\PlatformImages\">\\SOFS\Share\CRP\PlatformImages\</a>`
  2. For **ImagePath**, type the path to the PIR image. In my case ‘`C:\templates\Sysprep2008R2.vhd’`
  3. For **Publisher**, type a publisher name, like _Microsoft_.
  4. For **Offer**, type any value, like WindowsServer.
  5. For **Sku**, type a SKU for the image, like 2008-R2.
  6. For **Version**, type a version in #.#.# format, like _1.0.0_.
  7. For **OsType**, type _Windows_ or _Linux_.

**Make sure the -Offer and/or -SKU does not contain a space or the manifest will be invalid and a gallery item will not be created.**

We can now use the parameters above to launch the script:

[php].\CopyImageToPlatformImageRepository.ps1 -PlatformImageRespositoryPath &#92;SOFS\Share\CRP\PlatformImages\ -ImagePath ‘C:\templates\Sysprep2008R2.vhd’ -Publisher "Microsoft" -Offer "WindowsServer" -Sku "2008-R2" -Version 1.0.0 -OsType Windows –Verbose[/php]

  * Once complete navigate to [\\SOFS\Share\CRP\PlatformImages\](file://sofs/Share/CRP/PlatformImages/) and you will see your image with a manifest.json file.

[<img class="alignnone size-medium wp-image-13241" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/sofs-300x103.png" alt="sofs" width="300" height="103" srcset="/wp-content/uploads/2016/09/sofs-300x103.png 300w, /wp-content/uploads/2016/09/sofs-768x263.png 768w, /wp-content/uploads/2016/09/sofs.png 965w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/sofs.png)

[<img class="alignnone size-medium wp-image-13131" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image13-300x197.png" alt="image13.png" width="300" height="197" srcset="/wp-content/uploads/2016/09/image13-300x197.png 300w, /wp-content/uploads/2016/09/image13.png 670w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/image13.png)

After the command completes, restart your browser to see the new item in the Marketplace. The image can now be referenced in your virtual machine deployment templates. In some instances it may take up to 5 minutes for this new image to appear in the Marketplace.

[<img class="alignnone size-medium wp-image-13201" src="https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/stackimages-300x230.png" alt="stackimages" width="300" height="230" srcset="/wp-content/uploads/2016/09/stackimages-300x230.png 300w, /wp-content/uploads/2016/09/stackimages-768x588.png 768w, /wp-content/uploads/2016/09/stackimages-1024x784.png 1024w, /wp-content/uploads/2016/09/stackimages-240x185.png 240w" sizes="(max-width: 300px) 100vw, 300px" />](https://mscloudstorage.blob.core.windows.net/mscloudstorage/2016/09/stackimages.png)

&nbsp;

Thanks,

Alex
