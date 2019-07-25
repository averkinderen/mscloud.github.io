---
id: 5921
title: Enable Hyper-V Replica for all virtual machines in a specific Cloud
date: 2015-02-07T10:00:39+10:00
author: alexandre@verkinderen.com

guid: http://www.mscloud.be/?p=5921
permalink: /enable-hyper-v-replica-for-all-virtual-machines-in-a-specific-cloud/
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
  - "6619"
  - "6619"
  - "6619"
image: /wp-content/uploads/2015/02/replica1-150x140.jpg
categories:
  - SystemCenter
  - WAP
tags:
  - Hyper-V
  - powershell
  - SCVMM
  - VMM
  - WAP
---
As discussed in my [previous blog post](http://www.mscloud.be/create-virtual-networks-in-vmm-with-powershell/) I&#8217;m now working on a migration project to move virtual machines from one datacenter to another datacenter. I&#8217;m using Hyper-V Replica to replicate all the virtual machines with as less down-time as possible.

> Hyper-V Replica can asynchronously replicate a selected VM running at a primary site to a designated replica site across LAN/WAN. The following schematic presents this concept &#8211; See more at: http://blogs.technet.com/b/yungchou/archive/2013/01/10/hyper-v-replica-explained.aspx#sthash.MI4qs7oi.dpuf

The figure below shows how I&#8217;m using HyperV replica at my current customer:

&nbsp;

[<img class="alignnone size-full wp-image-5931" src="http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/replica.png" alt="replica" width="608" height="413" srcset="/wp-content/uploads/2015/02/replica.png 608w, /wp-content/uploads/2015/02/replica-300x204.png 300w, /wp-content/uploads/2015/02/replica-370x250.png 370w" sizes="(max-width: 608px) 100vw, 608px" />](http://mscloudstorage.blob.core.windows.net/mscloudstorage/2015/02/replica.png)

&nbsp;

The issue with Hyper-V Replica is that you need to configure the replication one by one in Hyper-V or in the Failover Cluster manager if you have clustered Hyper-V servers like me. However as Hyper-V Replica is a hyper-V feature you can use PowerShell to enable replication (more information on how to manage Hyper-V replica from Powershell can be found <a href="http://blogs.technet.com/b/matthts/archive/2012/04/02/managing-hyper-v-replica-from-powershell.aspx" target="_blank">here</a> ).

I have desinged a migration process for my customer so that I can migrate tenant per tenant (our cloud per cloud) to the new datacenter. To do this I need to be able to enable replication (and later planned Failover) per tenant or per cloud that are defined in VMM. Now that&#8217;s a challenge! 🙂

So I developed a PowerShell script that has the name of the Cloud I want to migrate as input and the name of the replica server to send the virtual machines. The script will:

  1. loop through all the VM&#8217;s in that cloud
  2. If replication is not enabled, enable replication
  3. connect to the hyperv host that is hosting the virtual machine at that moment
  4. launching a remote session to that host
  5. and start initial replication

The script has some variables in the beginning that you will have to change to reflect your own environment. Make sure you have configured replication before and that you have fully tested replication at least for one machine.You can download the whole script <a href="https://gallery.technet.microsoft.com/Enable-Hyper-V-Replica-for-5a73da94" target="_blank">here </a>and run it from your VMM server in PowerShell ISE.

[xml]

# PowerShell Enable replica per VMM Cloud

# Example usage:

# Authhor: Alexandre Verkinderen

#region Variables and Arguments  
#Define the Cloud that you would like to replicate. ALL VMs that are in that Cloud that are not yet replicated will be replicated to the HyperV Failover Replica Server.  
$CloudName = &#8216;test-alex&#8217;  
$ReplicaName = &#8216;ReplicaServerbroker.contoso.com&#8217;  
$ReplicaPort = 80  
$Auth = &#8216;Kerberos&#8217;  
#endregion

#Getting all vms in the cloud  
$VMs = @(Get-SCVirtualMachine | Where {$_.Cloud -like $CloudName})

#Loop through the vms and enable replication and start automatically the initial replication  
Foreach ($vm in $VMs)  
{  
$VMname = $vm.Name  
$VMhost = $vm.VMHost  
If ($Vm.IsPrimaryVM -Match &#8216;False&#8217;)

{  
Enable-VMReplication -VMName $vm.Name -ComputerName $VMhost -ReplicaServerName $ReplicaName -ReplicaServerPort $ReplicaPort -AuthenticationType $Auth -CompressionEnabled 1

Invoke-Command -computername $vm.VMHost -ScriptBlock{ param ($Name)  
Start-VMInitialReplication -VMName $Name  
} -Args $VMname  
Write-Host &#8216;Replica enabled for= &#8216; $VMname  
}  
Else  
{  
Write-Host &#8216;Replica already enabled for = &#8216;$VMname  
}  
}

[/xml]

The end-result will be that all my VM&#8217;s in a specific cloud are not being replicated to the other datacenter.  I just need to enable planned-failover to move them over but that will be for another weekend and another blogpost 🙂

Hope this helps,  
Alexandre
