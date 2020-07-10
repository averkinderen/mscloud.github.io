---
title: "Create an Automatic Service Principal Azure RM Service Connections in Azure DevOps via Azure CLI"
author: Rodney Almeida
categories:
  - Azure
tags:
  - Azure
  - Azure Devops
---

With more and more of our development projects being built and released via Azure DevOps, I find myself creating a few DevOps project which at start up share identical configs. Therefore this week I have been trying to automate this process. Many of the configs are easily configurable with AzureCLI and the Devops extention of it, but one thing I was struggling with was the creation of the service connections the way we do it from the GUI. We are using the Automatic Option when setting up the service principals for each of our Subscriptions.

![Automatic Service Connector GUI]({{ site.url }}/assets/images/2020-07-11-AutomaticGUI.PNG)

This is the preferred option as we don't then have to make certificates and keys etc. I wanted to be able to do the same thing with AzureCLI but if you look at the documentation there doesn't seem to be command for this. The ['az devops service-endpoint azurerm create'](https://docs.microsoft.com/en-us/cli/azure/ext/azure-devops/devops/service-endpoint/azurerm?view=azure-cli-latest#ext-azure-devops-az-devops-service-endpoint-azurerm-create) would seem to be the one we have to use but there is no automatic flag and its parameters are essentially what you see in the manual option on the GUI.

![Manual Service Connector GUI]({{ site.url }}/assets/images/2020-07-11-ManualGUI.PNG)

So it was looking like it was not going to be possible to automate that part until I started looking at the general ['az devops service-endpoint create'](https://docs.microsoft.com/en-us/cli/azure/ext/azure-devops/devops/service-endpoint?view=azure-cli-latest#ext-azure-devops-az-devops-service-endpoint-create) commands which requires a config file.

While doing some research online, I found various examples for creating Service Connection to numerous external and third party products but nothing to AzureRM. Using another project as a template i started using the the ['az devops service-endpoint list'](https://docs.microsoft.com/en-us/cli/azure/ext/azure-devops/devops/service-endpoint?view=azure-cli-latest#ext-azure-devops-az-devops-service-endpoint-list) and ['az devops service-endpoint show'](https://docs.microsoft.com/en-us/cli/azure/ext/azure-devops/devops/service-endpoint?view=azure-cli-latest#ext-azure-devops-az-devops-service-endpoint-show) commands to get the config of those connections in an effort to recreate the config and hopefully get it to create the automatic service principal connected we wanted. After some trial and error I go a config that successfully creates the service connection.

```json
{
  "data": {
    "creationMode": "Automatic",
    "environment": "AzureCloud",
    "managementGroupId": "",
    "managementGroupName": "",
    "mlWorkspaceLocation": "",
    "mlWorkspaceName": "",
    "oboAuthorization": "",
    "resourceGroupName": "",
    "resourceId": "",
    "scopeLevel": "Subscription",
    "subscriptionId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "subscriptionName": "DEV"
  },
  "description": "",
  "groupScopeId": null,
  "isReady": false,
  "isShared": false,
  "name": "SC-DEV",
  "authorization": {
    "parameters": {
      "authenticationType": "spnKey",
      "tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
    },
    "scheme": "ServicePrincipal"
  },
  "owner": "Library",
  "readersGroup": null,
  "type": "azurerm",
  "url": "https://management.azure.com/"
}
```

> Note: We tried to have this step run as part of a YAML Build Pipeline but the service connector is unable to create the SPN. In the GUI it looks like the Service Connection is created which confused us at first, but if use the 'az devops service-endpoint list' for that project it does not return any Service Connections. However, if you do a 'az devops service-endpoint show' and specify the ID of the service connector that is outputted during the 'az devops service-endpoint create' you will see the detail of the service connection.

> ![Failed SC Creation in Pipeline]({{ site.url }}/assets/images/2020-07-11-FailedPipelineRun.PNG)

> As you can see, the service connection is never completely provisioned as it is unable to create the SPN in AAD as it does not have rights to do so. This step is one of many that we have not being able to have run as a DevOps Pipeline due to similar reasons. Therefore we have opted you have the provisioning of a new DevOps Project run as a Powershell script which will run under the context of a real user who has the necessary rights to both Azure AD and DevOps.
