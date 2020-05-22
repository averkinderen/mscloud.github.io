---
title: "Use Azure DevOps Self Hosted agents with Azure App Service access restrictions"
categories:
  - Azure
tags:
  - Azure
  - Azure Devops
---

By default, when you deploy a new Azure WebApp, Function app or API app it will be publicly available to the internet. For the current customer I'm working on we made it a standard that all webapps should not be directly publicly available. To enhance our security we deploy Azure Frontdoor and Azure API Management Service for our APIs and also [enable IP restrictions](https://docs.microsoft.com/en-us/azure/app-service/app-service-ip-restrictions). As mentioned in my [previous blog post](https://mscloud.be/azure/Update-API-in-APIM-from-Azure-Devops/) we currently use Azure DevOps with Microsoft hosted agents to build and release all of our web apps and API apps.

## Issue

Our release pipeline broke after enabling IP restrictions on the API app.

![Devops error message]({{ site.url }}/assets/images/2020-05-15-AZDO-400.png)

We have a task, as mentioned in [this blogpost](https://mscloud.be/azure/Update-API-in-APIM-from-Azure-Devops), that reads the Swagger file from our API app to update the APIs in APIM. After enabling IP restrictions we would receive a 404 error message when trying to read the swagger file as the swagger file was not publicly availabile anymore

```json
2020-05-12T04:03:55.0921140Z 						}
2020-05-12T04:03:55.0965097Z Creating or updating API https://management.azure.com/subscriptions/xxxx/resourceGroups/RG-providers/Microsoft.ApiManagement/service/de/apis/xxxxx-client-api?api-version=2018-01-01
2020-05-12T04:03:56.5778313Z @{code=ValidationError; target=representation; message=Parsing error(s): Failed to import from specified resource https://api-d-xxxx.azurewebsites.net/swagger/v1/swagger.json: Response status code does not indicate success: 404 (Not Found)..}
2020-05-12T04:03:56.8939058Z ##[error]The remote server returned an error: (400) Bad Request.
2020-05-12T04:03:56.9309562Z ##[section]Finishing: Update API in APIM
```

So we had to try and find the public IP of our hosted agents and add those IPs in the allow list on our WebApp. At first I tried adding these [Azure Devops IP addresses](https://docs.microsoft.com/en-us/azure/devops/organizations/security/allow-list-ip-url?view=azure-devops#ip-addresses-and-range-restrictions) in the allow IP list of the webApp. However, the release pipeline still failed as those are the IP adddresses of the Azure DevOps Service itself, like the control plane. Not the build agents themselves.

I then realised the hosted agents are being deployed as resources in Azure in the same [Azure geography](https://azure.microsoft.com/en-us/global-infrastructure/geographies/) as your Azure DevOps Organization. So in my case, the hosted agents would be spin up in Azure EastUS 2.

![Devops region]({{ site.url }}/assets/images/2020-05-16-AZDO-region.png)

The list of [public IPs used per](https://www.microsoft.com/en-us/download/details.aspx?id=56519) region is updated every week. I would need to download this list every week and update my IP restrictions on a weekly basis with some kind of automation. This is definitely not something that I wanted to do.

> **NOTE**
> Due to some capacity restrictions in some regions your hosted agents may be deployed in other Azure Geographies as your Devops location. For example if there are capacity issues in West Europe the Hosted agents fall back to France. This would make it even more difficult to automate.

## Solution: Self Hosted Agents

I'm a big fan of Microsoft hosted agents, it makes my life easier, I don't need to worry about maintenance and high availability and it's really cheap to just buy another agent if needed. However, for this scenario the only possible solution is to use Self-Hosted build agents and add the public IP to the webApp IP restriction Allow List. There are a few different options to install a self-hosted agent ([docker](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops) and [Windows](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/v2-windows?view=azure-devops) for example) that I'm not going to cover here. We installed a self-hosted agent in our virtual network that is sitting behind an Azure Firewall in our Hub network and all subnets have that firewall defined as the next hope for route 0.0.0.0/0. This means that all unknown traffic (like internet traffic) will go through the Azure Firewall and will exit our network using the public IP of that Azure Firewall.

![Azdo Self Hosted]({{ site.url }}/assets/images/2020-05-16-AZDO-Selfhosted.png)

After deploying the self-hosted agent in our network all we had to do was to add the public ip of the Azure Firewall to our IP restrictions list and change our Yaml pipeline to use the self-hosted agent instead

```Yaml
- stage: DEV
  variables:
    - group: DEV
  displayName: "Release to DEV"
  jobs:
    - job: DEV
      displayName: "Deploy to DEV"
      pool: Self-Hosted
      steps:
      - task: DownloadBuildArtifacts@0
        displayName: "Download Build Artifact"
        inputs:
          buildType: 'current'
          downloadType: 'single'
          artifactName: 'drop'
          downloadPath: '$(System.ArtifactsDirectory)'
```

And adding the public IP to the allow list on the Azure APP:

![WebApp IP restrictions]({{ site.url }}/assets/images/2020-05-16-AZDO-IPrestrictions.png)

After this we could successfully read the swagger file from our APIapp and update the API management. :smile:

![Successfly read from swagger]({{ site.url }}/assets/images/2020-05-16-AZDO-200.png)

We also updated our ARM template that deploys our webApps to automatically add the public IP of the Azure Firewall to the allow list.

```json
"variables": {
    "newAppServicePlanName": "[take(concat('asp-', parameters('newAppServicePlanPrefix'),'-', uniqueString(parameters('guidValue'))),24)]",
    "webservicefarmname": "[if(parameters('deployAppServicePlan'),variables('newAppServicePlanName'),parameters('existingAppServicePlanName'))]",
    "copy": [
      {
        "name": "WebAppsTidy",
        "count": "[length(parameters('WebApps'))]",
        "input": {
          "name": "[take(concat(if(equals(tolower(trim(parameters('WebApps')[copyIndex('WebAppsTidy')].kind)), 'app'),'aps-','api-'),parameters('WebApps')[copyIndex('WebAppsTidy')].name,'-',uniqueString(parameters('guidValue'))),24)]",
          "Kind": "[parameters('WebApps')[copyIndex('WebAppsTidy')].kind]"
        }
      }
    ],
    "DevopsIP": "20.x.0.0/16",
    "PROD-vnetSubnetResourceId": "/subscriptions/xxxxxxf/resourceGroups/RG-xxxx/providers/Microsoft.Network/virtualNetworks/xxxx/subnets/xxxx",
    "AppIpSecurityRestrictions": [
      {
        "ipAddress": "[variables('DevopsIP')]",
        "action": "Allow",
        "priority": 100,
        "name": "Allow Devops"
      }
    ],
    "ApiIpSecurityRestrictions": [
      {
        "vnetSubnetResourceId": "[variables('vnetSubnetResourceId')]",
        "action": "Allow",
        "priority": 200,
        "name": "Allow APIM"
      }
    ]
  },
  "resources": [
    {
      "apiVersion": "2019-08-01",
      "type": "Microsoft.Web/serverfarms",
      "name": "[variables('newAppServicePlanName')]",
      "condition": "[parameters('deployAppServicePlan')]",
      "kind": "app",
      "location": "[parameters('location')]",
      "properties": {
      },
      "dependsOn": [
      ],
      "sku": {
        "name": "[parameters('sku')]"
      }
    },
    {
      "apiVersion": "2019-08-01",
      "type": "Microsoft.Web/sites",
      "copy": {
        "name": "sitesLoop",
        "count": "[length(parameters('WebApps'))]"
      },
      "kind": "[variables('WebAppsTidy')[copyIndex()].kind]",
      "name": "[variables('WebAppsTidy')[copyIndex()].name]",
      "location": "[parameters('location')]",
      "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('webservicefarmname'))]",
        "httpsOnly": true,
        "siteConfig": {
          "ipSecurityRestrictions": "[if(equals(variables('WebAppsTidy')[copyIndex()].kind,'app'),variables('AppIpSecurityRestrictions'),variables('ApiIpSecurityRestrictions'))]",
          "scmIpSecurityRestrictions": "[if(equals(variables('WebAppsTidy')[copyIndex()].kind,'app'),variables('AppIpSecurityRestrictions'),variables('ApiIpSecurityRestrictions'))]"
        }
      },
      "identity": {
        "type": "SystemAssigned"
      },
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('webservicefarmname'))]"
      ]
    }
```

Hope this helps,
Alex
