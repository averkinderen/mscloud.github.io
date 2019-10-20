---
title: "Debugging Windows Virtual Desktop Deployment Issues"
categories:
  - Azure
  - Windows Virtual Desktop
tags:
  - Azure
  - Windows Virtual Desktop
  - Azure Backup
  - Azure File share
---

This blog post is a part of a Windows Virtual Desktop series. In our last blog post we succesfully deployed WVD but what I didn't cover was the few issues I encountered when deploying the WVD template. This blog post will summarize the few issues I had and how to solve them.

* Part 1: [Installing Windows Virtual Desktop](https://mscloud.be/azure/windows%20virtual%20desktop/Installing-Windows-Virtual-Desktop/)
* Part 2: [Deployment issues](https://mscloud.be/azure/windows%20virtual%20desktop/Debugging-Windows-Virtual-Desktop-Deployment-issues/)

## Template Validation Failed

You might get an error message in the Azure portal saying that the WVD template deployment validation failed as seen here:
![WVD deployment failed]({{ site.url }}/assets/images/2019-10-14_WVD-Deployment-failed.png)
The error message mentioned above doesn't make any sense at all and doesn't provide more detail in the portal. So you need to use get-azlog if you get the above error message. Normally you would use the provided tracking ID and use it like this:

```PowerShell
Get-AzLog -CorrelationId '60c694d0-e46f-4c12-bed1-9b7aef541c23'
```

In case you don't get anything back (like me), use the following to get all events that happened against the resource group where the host pool will be created:

```PowerShell
Get-AzLog -ResourceGroupName "Contoso-WVD"
```

That's how I discovered the following error message:
![WVD Quota Exceeded]({{ site.url }}/assets/images/2019-10-21_WVD-Quota-Exceeded.png)
This one was an easy fix. Apparently I was exceeding the allowed cores per subscription per region.

## Failed Domain Join

Our next error was related to the domain join of the virtual machines. With Windows Virtual Desktop you have either the option to use Azure Active Directory Domain Services or Active Directory. I chose the latter.

1. Make sure your VNET that you use to deploy your Virtual Machines has access to the domain controllers.
2. Make sure you have the appropriate credentials to join your machines to the domain
3. Check the VNET is using custom DNS and point to your domain controllers
4. In my case I had the appropriate username and password and the user was able to join machines to the domain but only to one specific OU so I got the following error:

![WVD domain join fail]({{ site.url }}/assets/images/2019-10-21_WVD-DomainJoin-Fail.png)

I had to go back to the HostPool deployment settings and specify the Domain and the OU in the following format:

'OU=wvd,DC=abccorp,DC=abccorp,DC=com'

![WVD Specify ou]({{ site.url }}/assets/images/2019-10-21_WVD-SpecifyOU.jpg)
And as we can see now, the extension was succesfully deployed and configured:
![WVD DSC Success]({{ site.url }}/assets/images/2019-10-21_WVD-DSC-success.png)
Let's check on the VM itself:
![WVD domain join]({{ site.url }}/assets/images/2019-10-15_WVD-VMdomainjoin.png)

Alex
