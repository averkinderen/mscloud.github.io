---
id: 19822
title: Getting started with the Azure Iot DevKit
date: 2017-12-14T09:43:34+10:00
author: alexandre@verkinderen.com

guid: http://mscloud.be/?p=19822
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
  - "2964"
categories:
  - Azure
  - IOT
tags:
  - Azure
  - Devkit
  - Iot
---
I finally got my hands on some Azure IoT Developer kits! In this blogpost I will cover how to get started with the Devkit, make sure it’s connected to the internet, upgrade the firmware and install all the prerequisites on your computer.

[<img style="display: inline; background-image: none;" title="devkit" src="http://mscloud.be/wp-content/uploads/2017/12/devkit_thumb.jpg" alt="devkit" width="244" height="158" border="0" />](http://mscloud.be/wp-content/uploads/2017/12/devkit.jpg)

## Introduction

The IoT Development Kit is based on the [MXChip AZ3166](http://mxchip.com/az3166) board. The AZ3166 board is Arduino compatible with a very large number of peripherals and sensors built directly on the board. This board is being built as an ideal platform for prototyping IoT and Smart Device solutions. The main control unit of the AZ3166 is a EMW3166-a low power consumption Wi-Fi module developed by MXCHIP. With a DAP Link emulator and 128×64 OLED and other resources such as LED lights. The development kit has an audio processing unit to connect to Azure for voice recognition and voice play. The full list of all features:

  * EMW3166 Wifi module with 256K SRAM,1M+2M Byte SPI Flash
  * DAP Link emulator
  * MicroUSB
  * 3.3V DC-DC,maximum current 1.5A
  * Codec,with ,microphone and earphone socket
  * OLED,128×64
  * 2 user button
  * 1 RGB light
  * 3 working status indicator
  * Security encryption chip
  * Infrared emitter
  * Motion sensor
  * Magnetometer sensor
  * Atmospheric pressure sensor
  * Temperature and humidity sensor
  * Connecting finger extension interface

[<img style="display: inline; background-image: none;" title="mxweb-12" src="http://mscloud.be/wp-content/uploads/2017/12/mxweb-12_thumb.png" alt="mxweb-12" width="237" height="244" border="0" />](http://mscloud.be/wp-content/uploads/2017/12/mxweb-12.png)

## Getting started

IoT projects rely on internet connectivity. <span style="display: inline !important; float: none; background-color: transparent; color: #333333; cursor: text; font-family: Georgia,'Times New Roman','Bitstream Charter',Times,serif; font-size: 16px; font-style: normal; font-variant: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: left; text-decoration: none; text-indent: 0px; text-transform: none; -webkit-text-stroke-width: 0px; white-space: normal; word-spacing: 0px;">So the first thing you will need to do is configuring your IoT devkit to connect to your wireless network. </span>

[<img style="display: inline; background-image: none;" title="nowifi" src="http://mscloud.be/wp-content/uploads/2017/12/nowifi_thumb.jpg" alt="nowifi" width="184" height="244" border="0" />](http://mscloud.be/wp-content/uploads/2017/12/nowifi.jpg)

Hold down button B, push and release the reset button, and then release button B. Your DevKit enters accespoint or AP mode for configuring Wi-Fi. The screen displays the service set identifier(SSID) of the DevKit and the configuration portal IP address:



Then connect to the new wireless using your laptop

<img class="alignnone size-medium wp-image-19835" src="/wp-content/uploads/2017/12/ap-178x300.png" alt="" width="178" height="300" srcset="/wp-content/uploads/2017/12/ap-178x300.png 178w, /wp-content/uploads/2017/12/ap.png 365w" sizes="(max-width: 178px) 100vw, 178px" /> 

<span style="display: inline !important; float: none; background-color: transparent; color: #333333; cursor: text; font-family: Georgia,'Times New Roman','Bitstream Charter',Times,serif; font-size: 16px; font-style: normal; font-variant: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: left; text-decoration: none; text-indent: 0px; text-transform: none; -webkit-text-stroke-width: 0px; white-space: normal; word-spacing: 0px;">and browse to the IP address shown in the screen of your DevKit:</span>

[<img style="display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/12/image_thumb.png" alt="image" width="244" height="130" border="0" />](http://mscloud.be/wp-content/uploads/2017/12/image.png)

Select the Wi-Fi network that you want the DevKit to connect to, and then type the password. Select Connect**.** As soon as you do this the Devkit will try and connect to your wireless network:

[<img style="display: inline; background-image: none;" title="connecting" src="http://mscloud.be/wp-content/uploads/2017/12/connecting_thumb.jpg" alt="connecting" width="184" height="244" border="0" />](http://mscloud.be/wp-content/uploads/2017/12/connecting.jpg)

When the connection succeeds, the DevKit reboots in a few seconds. You then see the Wi-Fi name and IP address on the screen

[<img style="display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/12/image_thumb-1.png" alt="image" width="244" height="130" border="0" />](http://mscloud.be/wp-content/uploads/2017/12/image-1.png)

## Upgrading the firmware

As soon as the Devkit connects to the internet it will check if there is a new firmware available. As you can see my firmware was not the latest one so I quickly upgraded it to the latest version:

[<img style="display: inline; background-image: none;" title="connectiondone" src="http://mscloud.be/wp-content/uploads/2017/12/connectiondone_thumb.jpg" alt="connectiondone" width="184" height="244" border="0" />](http://mscloud.be/wp-content/uploads/2017/12/connectiondone.jpg)

Download the latest version from <a href="https://aka.ms/devkit/prod/firmware/latest" target="_blank" rel="noopener">here</a>.

  1. Drag & drop the .bin file you downloaded to AZ3166 device.

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/12/image_thumb-2.png" alt="image" width="244" height="37" border="0" />](http://mscloud.be/wp-content/uploads/2017/12/image-2.png)

Wait until the file is copied, then the DevKit will reboot to the latest firmware.

  1. After this is done, you will see the new firmware version on the screen of the kit.

[<img style="display: inline; background-image: none;" title="latestfirmware" src="http://mscloud.be/wp-content/uploads/2017/12/latestfirmware_thumb.jpg" alt="latestfirmware" width="184" height="244" border="0" />](http://mscloud.be/wp-content/uploads/2017/12/latestfirmware.jpg)

## Prepping your development environment

You will need to download the latest development environment from <a href="https://aka.ms/devkit/prod/installpackage/latest" target="_blank" rel="noopener">here</a>. The zip file contains the following tools and packages:

If you already have some of them installed, the script will can and skip them.

  * Node.js and Yarn: Runtime for the setup script and automated tasks.
  * [Azure CLI 2.0 MSI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest#install-on-windows) &#8211; Cross-platform command-line experience for managing Azure resources. The MSI contains dependent Python and pip.
  * [Visual Studio Code](https://code.visualstudio.com/) (VS Code): Lightweight code editor for DevKit development.
  * [Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Extension that enables Arduino development in Visual Studio Code.
  * [Arduino IDE](https://www.arduino.cc/en/Main/Software): The extension for Arduino relies on this tool.
  * DevKit Board Package: Tool chains, libraries, and projects for the DevKit
  * ST-Link Utility: Essential tools and drivers.

During installation, you can see the progress of each tool or package being installed

[<img style="margin: 0px; display: inline; background-image: none;" title="image" src="http://mscloud.be/wp-content/uploads/2017/12/image_thumb-3.png" alt="image" width="244" height="130" border="0" />](http://mscloud.be/wp-content/uploads/2017/12/image-3.png)

## Sensors

Now that we have everything installed and up and running, let&#8217;s test the built in sensors. Just press the button B once to test the sensors:



Teaser: I&#8217;m going send the data generated by the sensors to IoT hub later on.

## Conclusion

It was really easy to configure my Azure Iot Devkit and connect it to the internet. In less than 30 minutes everything was connected, upgraded and installed. In fact it took me longer to write this blogpost than to get started with the Azure Iot Devkit.

I will experiment with some cool projects in the next coming days/weeks and connect my Devkit to Azure IotHub . So stay tuned for some exciting experiments!
