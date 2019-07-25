---
id: 5271
title: Create Virtual networks in VMM with Powershell
date: 2015-01-31T08:27:58+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=5271
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
  - "6442"
  - "6442"
  - "6442"
image: /wp-content/uploads/2015/01/logical-network-150x150.png
categories:
  - SystemCenter
tags:
  - network
  - Networking
  - powershell
  - SCVMM
  - VMM
---
I&#8217;m now working on a HyperV migration project to move all servers from one datacenter to a new datacenter. This implies that I need to move all virtual machines with HyperV replica, configure virtual networks in the new datacenter etc.

My customer is using VLAN Isolation in VMM. For more information about Network isolation have a look <a href="http://blogs.technet.com/b/scvmm/archive/2013/05/22/logical-networks-part-iii-network-isolation.aspx" target="_blank">here</a>.  Service Providers often use dedicated VLANs and PVLANs to isolate different tenants from one another.  As described in <a href="http://blogs.technet.com/b/scvmm/archive/2013/05/22/logical-networks-part-iii-network-isolation.aspx" target="_blank">the blog post </a>I&#8217;m using **one** logical network for _all_ of the tenants, and configure sites, vlans and networks per tenant. Multiple VM networks may be linked to the same Logical Network if _Network Virtualization_ is enabled, with each one of these VM Networks separated from and totally unaware of the existence of any of the others. But if you have a lot tenants this is a lot of manual work 🙂

As I couldn&#8217;t reuse the old VMM server and config in the new datacenter for several reasons I have to re-configure the networking (Vlans, subnets, network sites, etc)  configuration from scratch. So  I found a way to automate all of this labour intensive tasks with Powershell.

This blogpost is not about how to configure step by step networking in VMM, if you need more information on how to configure networking in vmm have a look <a href="http://charbelnemnom.com/2014/05/create-a-converged-network-fabric-in-vmm-2012-r2" target="_blank">here </a> or <a href="https://gallery.technet.microsoft.com/Hybrid-Cloud-with-NVGRE-aa6e1e9a" target="_blank">download </a>the Networking white paper from Kristian Nese .

The key thing to be able to keep an overview (if you are using networking in VMM) and for easy troubleshooting is NAMING CONVENTION. Without a proper naming convention it will be very hard to now which VMnetwork is connected to which site and using this vlan or this subnet&#8230;

So I&#8217;m using the following naming convention:

  * Logical Network Name = &#8220;Customer &#8211; Logical Network &#8211; Name&#8221;
  * Network Site = &#8220;Customer + VLANname + Site + VLanID&#8221;
  * Virtual Network Name =  &#8220;Customer + VLANname + VMNetwork + VLanID&#8221;
  *  SubnetName = &#8220;Customer + VLANname + VMSubnet+ VLanID&#8221;
  * etc

You get the point.

&nbsp;

Now let&#8217;s get started!

First of all the the script assumes you already have a Logical network defined using VLAN based indepentend networks.

[<img class="alignnone wp-image-5301 size-large" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/logical-network-1024x171.png" alt="logical network" width="768" height="128" srcset="/wp-content/uploads/2015/01/logical-network-1024x171.png 1024w, /wp-content/uploads/2015/01/logical-network-300x50.png 300w, /wp-content/uploads/2015/01/logical-network-768x128.png 768w, /wp-content/uploads/2015/01/logical-network.png 1597w" sizes="(max-width: 768px) 100vw, 768px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/logical-network.png)

&nbsp;

Open Powershell ISE and copy past the script. Next you just change the following variables in the scrip to match your own:

[xml]  
<pre>$Subnet = "10.100.40.10/24"  
$VlanID = 521  
$VlanName = "ITSystems"  
$Customer = "Contoso"</pre>  
[/xml]

The end result is:

  * All my network sites are created with proper naming convention
  * Associated Vlans and subnet defined

[<img class="alignnone wp-image-5311 size-large" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/network-sites-1024x519.png" alt="network sites" width="768" height="389" srcset="/wp-content/uploads/2015/01/network-sites-1024x519.png 1024w, /wp-content/uploads/2015/01/network-sites-300x152.png 300w, /wp-content/uploads/2015/01/network-sites-768x390.png 768w, /wp-content/uploads/2015/01/network-sites.png 1463w" sizes="(max-width: 768px) 100vw, 768px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/network-sites.png)

and Virtual Networks created:

[<img class="alignnone wp-image-5321 size-large" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/vmnetworks-1024x251.png" alt="vmnetworks" width="768" height="188" srcset="/wp-content/uploads/2015/01/vmnetworks-1024x251.png 1024w, /wp-content/uploads/2015/01/vmnetworks-300x74.png 300w, /wp-content/uploads/2015/01/vmnetworks-768x188.png 768w" sizes="(max-width: 768px) 100vw, 768px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/01/vmnetworks.png)

and Port Profile changed as well.

&nbsp;

<pre>Below you can find the whole script:</pre>

[xml]

# PowerShell Script to configure Networking in VMM

#

# The script assumes you already have defined your networkig in VMM as explained here for examaple http://charbelnemnom.com/2014/05/create-a-converged-network-fabric-in-vmm-2012-r2/

# Once this is done and you have your logical network, your logical swtich and your port profile, you need to create sites and VLAN per tenant if your using VLAN isolation

# So the next labour intensive task is to create sites,vlans, subnet, reconfigure the portprofile with new site ,create a virtual network etc manually.

# Auhtor: Alexandre Verkinderen

#Get Variable  
#Specify your existing Logical network name  
$NetworkName = "Contoso &#8211; Logical Network &#8211; Tenants"  
#Specify your existing PortProfile.  
$portProfile = Get-SCNativeUplinkPortProfile -Name "Contoso &#8211; Reference &#8211; Profile" -ID "a3c36703-4e0b-4b25-baa7-69b347be8c72"  
#Specify the new subnet, the new vlan ID and a Name for the new network site  
############################  
$Subnet = "10.100.40.10/24"  
$VlanID = 521  
$VlanName = "ITSystems"  
$Customer = "Contoso"  
############################

$NetworkSiteName = $Customer + " &#8211; " + $VlanName+ " &#8211; Site &#8211; " + $VlanID  
$VMNetworkName = $Customer + " &#8211; " +$VlanName+ " &#8211; VMNetwork &#8211; " + $VlanID  
$VMSubnetName = $Customer + " &#8211; " + $VlanName+ " &#8211; VMSubnet &#8211; " + $VlanID

#First we get the Logical network that has already been created  
$logicalNetwork = Get-SCLogicalNetwork | Where {$_.Name -Match $NetworkName }  
#The Set-SCLogicalNetwork cmdlet changes the properties of a System Center Virtual Machine Manager (VMM) logical network object.  
Set-SCLogicalNetwork -Name $NetworkName -Description "" -LogicalNetwork $logicalNetwork -RunAsynchronously -EnableNetworkVirtualization $false -UseGRE $false -LogicalNetworkDefinitionIsolation $true  
#We are defining the new network settings for the All hosts group. If you need more granularity you can specify other host group names here  
$allHostGroups = @()  
$allHostGroups += Get-SCVMHostGroup | Where {$_.Name -Match "All Hosts" }  
$allSubnetVlan = @()  
$allSubnetVlan += New-SCSubnetVLan -Subnet $Subnet -VLanID $VlanID

#CreateSite  
#he New-SCLogicalNetworkDefinition cmdlet creates a definition for a System Center Virtual Machine Manager (VMM) logical network. The logical network can be associated with one or more host groups. A logical network definition is also called a network site.  
#After you create a new logical network, use the logical network definitinon to assign IP subnets and VLANs to the logical network.  
New-SCLogicalNetworkDefinition -Name $NetworkSiteName -LogicalNetwork $logicalNetwork -VMHostGroup $allHostGroups -SubnetVLan $allSubnetVlan -RunAsynchronously  
Write-Output "Site ok"

#CreateVMNetwork  
#The New-SCVMNetwork cmdlet creates a virtual machine network. Virtual machine networks support multiple methods of isolation: No isolation, network virtualization, external, and VLAN  
$vmNetwork = New-SCVMNetwork -Name $VMNetworkName -LogicalNetwork $logicalNetwork -IsolationType "VLANNetwork"

$logicalNetworkDefinition = Get-SCLogicalNetworkDefinition -Name $NetworkSiteName -LogicalNetwork $logicalNetwork  
$subnetVLAN = New-SCSubnetVLan -Subnet $Subnet -VLanID $VlanID  
$vmSubnet = New-SCVMSubnet -Name $VMSubnetName -LogicalNetworkDefinition $logicalNetworkDefinition -SubnetVLan $subnetVLAN -VMNetwork $vmNetwork  
Write-Output "VMNetwork ok"

#ChangePortProfile  
$logicalNetworkDefinitionsToAdd = @()  
$logicalNetworkDefinitionsToAdd += Get-SCLogicalNetworkDefinition -Name $NetworkSiteName  
Set-SCNativeUplinkPortProfile -NativeUplinkPortProfile $portProfile -Name "Contoso &#8211; Reference &#8211; Profile" -Description "" -EnableNetworkVirtualization $true -LBFOLoadBalancingAlgorithm "Dynamic" -LBFOTeamMode "SwitchIndependent" -RunAsynchronously -AddLogicalNetworkDefinition $logicalNetworkDefinitionsToAdd  
Write-Output "Profile Changed"  
[/xml]

You can also download the whole script from here: <a href="https://gallery.technet.microsoft.com/Configure-Virtual-Machine-a362f121" target="_blank">https://gallery.technet.microsoft.com/Configure-Virtual-Machine-a362f121</a>

Hope this helps,

Alexandre Verkinderen
