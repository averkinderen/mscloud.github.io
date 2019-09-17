---
title: "Move Azure File share backups to other Recovery Vault"
categories:
  - Azure
tags:
  - Azure
  - Storage Account
  - Azure Backup
  - Azure File share
---

Azure Backup let's you backup [Azure File shares](https://docs.microsoft.com/en-us/azure/backup/backup-azure-files) which is currently in preview. This article will describe how to move your Azure File share to another Recovery Vault.

## Intro

My current customer had about 15 Recovery Vaults which they wanted to consolidate into just one Vault. Moving backups for Azure Virtual Machines to another Vault is rather easy, you just stop the backup and add the virtual machine again in the other Vault. However, the same process doesn't apply if you have backups for Azure File share.

## Issue

I stopped the backup of my File share as [explained here](https://docs.microsoft.com/en-us/azure/backup/backup-azure-files#stop-protecting-an-azure-file-share) and tried to reprotect the File share into my new Recovery Vault but the Storage Account was not visible from my new Vault.

Currently, Microsoft is linking the Storage Account to the Recovery vault in order to avoid duplicate backups of File shares. So, even though I deleted the backup without retaining the data of my File share, the link between the Storage Account and the Recovery Vault still existed somewhere.

## Solution

Microsoft told me the solution was to first un-register the Storage Account from the old Vault.

![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/2019-09-13_14-16-47-unregister-sa.png)

Be carefull when doing this as this will delete all your file share backups.

Now that the link has been removed between the old Recovery Vault and the Storage Account we can register the Storage Account to the new Vault and add the File share.

![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/2019-09-13_14-18-43-registring-sa.png)

As you can see when we select the Storage Account where our File share is it will be registered and linked to the Recovery vault.

![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/2019-09-13_Fileshare.png)

## Conclusion

This is an undocumented feature, so big thanks to the Azure Storage and Backup product team to help out. Especially Klaas Langhout and Nikhil Kumar Raparthi.
