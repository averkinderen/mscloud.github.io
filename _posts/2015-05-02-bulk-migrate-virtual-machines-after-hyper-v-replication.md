---
id: 8691
title: Bulk migrate virtual machines after Hyper-V replication
date: 2015-05-02T06:35:55+10:00
author: alexandre@verkinderen.com
layout: post
guid: http://www.mscloud.be/?p=8691
permalink: /bulk-migrate-virtual-machines-after-hyper-v-replication/
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
  - "5832"
  - "5832"
  - "5832"
image: /wp-content/uploads/2015/05/replicafeatured-150x104.png
categories:
  - Powershell
  - SystemCenter
  - WAP
tags:
  - Hyper-V
  - powershell
  - SCVMM
  - WAP
---
As discussed in one of my [previous blog posts ](http://www.mscloud.be/enable-hyper-v-replica-for-all-virtual-machines-in-a-specific-cloud/)I’m now working on a migration project to move virtual machines from one datacenter to another datacenter. I’m using Hyper-V Replica to replicate all the virtual machines with as less down-time as possible. Now the issue with Hyper-V replica is that you can only replicate to one and only one storage location. In the settings as seen below you can only define one location:

[<img class="alignnone size-medium wp-image-8701" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/04/Hyper-V-Replica-ConfigureTargetHost-300x283.png" alt="Hyper-V-Replica location" width="300" height="283" srcset="/wp-content/uploads/2015/04/Hyper-V-Replica-ConfigureTargetHost-300x283.png 300w, /wp-content/uploads/2015/04/Hyper-V-Replica-ConfigureTargetHost.png 738w" sizes="(max-width: 300px) 100vw, 300px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/04/Hyper-V-Replica-ConfigureTargetHost.png)

My advise for Hyper-V replica (if you are using it like me as a temporary solution to migrate from one datacenter to another) is to have a temporary migration LUN to replicate the virtual machines. After the migration you can then just delete the temporary LUN.

Now this customer has a policy of separating LUNS per operating system for several technical (like speed of disks, different backup procedures, etc) and phylosophic (they don&#8217;t like to put all their eggs in the same basket) reasons. So this means I have 1 lun for Windows Clients, 1 lun for Windows server 2012, 1 lun for Windows server 2008, 1 for SQL servers, etc. Sadly enough after each planned failover from one datacenter to the other I need to do a manual storage migration of the virtual machine in VMM to the corresponding LUN on the new Hyper-V Cluster based  on the operating system. So I need to perform the following manual steps for each machine after the failover:

  1. Connect to the new hyperV cluster
  2. Verify planned fail over was succesfull
  3. Remove replication for the machine in Failover Clustermanager
  4. Connect to the VMM console
  5. Identify the operating system version of the migrated VM
  6. Perform a <a href="https://technet.microsoft.com/en-us/library/jj860433.aspx" target="_blank">quick storage migration </a>to the corresponding LUN based on the operating system of the virtual machine.
  7. and wait&#8230;.

This are a lot of manual steps and a lot of waiting time as well!!!

So I created a PowerShell script based on the <a href="http://vniklas.djungeln.se/2015/02/17/vm-storage-migration-in-vmm-2012-r2-leaves-unwanted-leftovers/" target="_blank">VM storage Migration script</a> from Niklas Akerlund. The script will:

  1. Connect to VMM
  2. Get all running Virtual machines
  3. Identify virtual machines that have a disk on the temporary LUN
  4. Connect to the host of the VM and remove Hyper-V replica for the machine
  5. Start a Quick storage migration **asynchronous** job in VMM (you need to use the &#8211;**asynchronous** option otherwise the script will not continue and not launch another job until the first one is finished)

Now let&#8217;s discuss the parameters needed for the script to be able to run:

[xml]  
#variables

$lun2012 = "C:\ClusterStorage\sata\_w2k12r2\_OS_ds1"  
$lun2008 = "C:\ClusterStorage\sata\_w2k8r2\_os_ds3"  
$lun2003 = "C:\ClusterStorage\sata\_w2k3\_os_ds1"  
$lunmig = "C:\ClusterStorage\sata\_migration\_ds1"  
$lunclients = "C:&#92;ClusterStorage&#92;sata\_clients\_ds1"  
$VMHostGroup = "All Hosts"  
$VMHostCluster = "cluster1"  
$VMHost = $null  
$maxjobs = 10

[/xml]

  * $lun2012 etc are variables that define my Cluster Shared volumes
  * $Lunmig is the location of my temporary LUN that Hyper-V replica is using to replicate the VM&#8217;s. Please note the double \\ for the lunmig variable
  * $MaxJobs is used to defined how many simultaneous storage migration your Hyper-V can take. If you want to know more about what this number should be have a <a href="http://www.aidanfinn.com/?p=12729" target="_blank">look here</a>.  So if in Hyper-V you have configured a limit of 2 set the $MaxJobs to 2 as well.

[<img class="alignnone size-medium wp-image-8741" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/04/Capture-300x286.png" alt="maxjobs" width="300" height="286" srcset="/wp-content/uploads/2015/04/Capture-300x286.png 300w, /wp-content/uploads/2015/04/Capture.png 729w" sizes="(max-width: 300px) 100vw, 300px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/04/Capture.png)

&nbsp;

Please find below the script:

[xml]</pre>  
&nbsp;

<#  
.Synopsis  
Storage Migration of VMM VM and also remove hyperv-replication if -removereplica is used.

More information can be found here: http://mscloud.be/bulk-migrate-virtual-machines-after-hyper-v-replication

.NOTES  
Author: Alexandre Verkinderen  
#>  
#region Variables  
#variables

#define CSV locations  
$lun2012 = "C:\ClusterStorage\sata\_w2k12r2\_OS_ds1"  
$lun2008 = "C:\ClusterStorage\sata\_w2k8r2\_os_ds1"  
$lun2003 = "C:\ClusterStorage\sata\_w2k3\_os_ds1"  
$lunmig = "C:&#92;ClusterStorage&#92;sata\_migration\_ds1"  
$lunclients = "C:\ClusterStorage\sata\_clients\_ds1"  
#define LOG location  
$LogFile = "C:\Users\verkinderenal\Downloads\log.csv"  
#define host group in vmm and hyperv clustername  
$VMHostGroup = "All Hosts"  
$VMHostCluster = "srvcluster1"  
$VMHost = $null  
#define max simultaneous Storage migrations  
$maxjobs = 10  
$VMHosts = (Get-SCVMHostCluster -Name $VMHostCluster).Nodes  
#get all running vms, we don&#8217;t want any vm&#8217;s that are still being replicated  
$VMs = $VMHosts | Get-SCVirtualMachine | where {$_.Status -eq &#8216;Running&#8217;}  
#endregion

function Move-SCVirtualMachineStorage  
{  
[CmdletBinding()]  
Param  
(  
[Parameter(Mandatory=$true,ParameterSetName="VMName")]  
[string[]]$VMName,  
[Parameter(Mandatory=$true,ParameterSetName="VM",ValueFromPipelineByPropertyName=$true)]  
[Microsoft.SystemCenter.VirtualMachineManager.VM]$VM,  
[ValidateNotNullOrEmpty()]$VMHost,  
[ValidateNotNullOrEmpty()]$Path,  
[boolean]$HighAvailable = $true,  
[switch]$RemoveReplica  
)

# Generate a GUID for the JobGroupID variable.

$JobGroupID = [Guid]::NewGuid().ToString()  
$VMHost = Get-SCVMHost -ComputerName $VMHost  
if ($VMName -ne $null){  
$VMs = @()  
foreach ($VMNamed in $VMName){  
$VMs += Get-SCVirtualMachine -Name $VMNamed  
}  
}else{  
$VMs = $VM  
}  
foreach($VM in $VMs){

#remove replica for the VM on the new host  
if($RemoveReplica){  
$hostname = $VM.HostName  
$machine = $vm.Name  
$script = {param($hostname,$machine); Remove-VMReplication -VMName $machine -ComputerName $hostname -ErrorAction SilentlyContinue}  
Invoke-Command -ComputerName $VM.HostName -ScriptBlock $script -ArgumentList $hostname,$machine  
#end scriptblock  
} #endif removereplica  
Start-sleep -Seconds 60  
Move-SCVirtualMachine -VM $VM -VMHost $VM.HostName -UseDiffDiskOptimization -HighlyAvailable $HighAvailable -Path $Path -JobGroup $JobGroupID -RunAsynchronously  
} #end foreach vm  
}  
foreach ($VM in $VMs) {

#run through all the vms but only continue if we didnt reach the max concurent jobs  
While((Get-SCJob | where { $_.Status -eq "Running" }).Count -ge $maxjobs)  
{  
Add-Content $LogFile "waiting"  
Start-Sleep -seconds 60  
} #end while

$VHDs = $VM | Get-SCVirtualDiskDrive  
foreach ($VHDconf in $VHDs){  
if ($VHDconf.VirtualHardDisk.HostVolume -match $lunmig ){  
if($VM.OperatingSystem -LIKE "_Unknown_"){  
Add-Content $LogFile "Migrating $VM.Name not possible as OS is Unknown"  
}  
Elseif($VM.OperatingSystem -like "_Windows 7"){  
Add-Content $LogFile "Migrating $VM.Name from $VHDconf.VirtualHardDisk.HostVolume.Name to $lunclients "  
Move-SCvirtualMachineStorage -VMName $VM.Name -VMHost $vm.HostName -Path $lunclients -RemoveReplica  
}  
Elseif($VM.OperatingSystem -like "_Windows Server 2012_"){  
Add-Content $LogFile "Migrating $VM.Name from $VHDconf.VirtualHardDisk.HostVolume.Name to $lun2012"  
Move-SCvirtualMachineStorage -VMName $VM.Name -VMHost $vm.HostName -Path $lun2012 -RemoveReplica  
}  
Elseif($VM.OperatingSystem -like "_Windows Server 2008_"){  
Add-Content $LogFile "Migrating $VM.Name from $VHDconf.VirtualHardDisk.HostVolume.Name to $lun2008"  
Move-SCvirtualMachineStorage -VMName $VM.Name -VMHost $vm.HostName -Path $lun2008 -RemoveReplica  
}  
Elseif($VM.OperatingSystem -like "_Windows 8_"){  
Add-Content $LogFile "Migrating $VM.Name from $VHDconf.VirtualHardDisk.HostVolume.Name to $lunclients "  
Move-SCvirtualMachineStorage -VMName $VM.Name -VMHost $vm.HostName -Path $lunclients -RemoveReplica  
}  
Elseif($VM.OperatingSystem -like "_Windows XP_"){  
Add-Content $LogFile "Migrating $VM.Name from $VHDconf.VirtualHardDisk.HostVolume.Name to $lunclients "  
Move-SCvirtualMachineStorage -VMName $VM.Name -VMHost $vm.HostName -Path $lunclients -RemoveReplica  
}  
Elseif($VM.OperatingSystem -like "_Windows Vista_"){  
Add-Content $LogFile "Migrating $VM.Name from $VHDconf.VirtualHardDisk.HostVolume.Name to $lunclients "  
Move-SCvirtualMachineStorage -VMName $VM.Name -VMHost $vm.HostName -Path $lunclients -RemoveReplica  
}  
Elseif($VM.OperatingSystem -like "_Windows Server 2003*"){  
Add-Content $LogFile "Migrating $VM.Name from $VHDconf.VirtualHardDisk.HostVolume.Name to $lun2003"  
Move-SCvirtualMachineStorage -VMName $VM.Name -VMHost $vm.HostName -Path $lun2003 -RemoveReplica  
}  
}#endif lunmig  
else {  
Add-Content $LogFile "No need to migrate $VM.Name"  
}

} #end foreach  
}

&nbsp;  
<pre>[/xml]

Launch the script on your VMM server and that&#8217;s it!

[<img class="alignnone size-medium wp-image-8921" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/05/vmmreplica-300x244.png" alt="vmmreplica" width="300" height="244" srcset="/wp-content/uploads/2015/05/vmmreplica-300x244.png 300w, /wp-content/uploads/2015/05/vmmreplica-768x623.png 768w, /wp-content/uploads/2015/05/vmmreplica.png 850w" sizes="(max-width: 300px) 100vw, 300px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/05/vmmreplica.png)

This is what I call:  
<img class="alignnone size-medium wp-image-8711" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/04/2015-01-26-21.47.43-300x143.png" alt="nailed it" width="300" height="143" srcset="/wp-content/uploads/2015/04/2015-01-26-21.47.43-300x143.png 300w, /wp-content/uploads/2015/04/2015-01-26-21.47.43-768x367.png 768w, /wp-content/uploads/2015/04/2015-01-26-21.47.43.png 843w" sizes="(max-width: 300px) 100vw, 300px" /> 

You can download the script here <a href="https://gallery.technet.microsoft.com/VMM-bulk-storage-migration-ad2184c0" target="_blank">https://gallery.technet.microsoft.com/VMM-bulk-storage-migration-ad2184c0 </a>

Hope this helps,

Alexandre Verkinderen