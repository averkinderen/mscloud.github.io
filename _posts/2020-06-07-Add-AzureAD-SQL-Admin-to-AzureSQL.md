---
title: "Setting an Azure AD group to Azure SQL Database with ARM templates"
categories:
  - Azure
tags:
  - Azure
  - Azure Devops
header:
  og_image: /assets/images/2020-06-06-AzureSQL-SetADadmin.png
---

I was recently looking at a way to automatically set an Azure AD group as the SQL admin for our Azure SQL databases with ARM tempplates. We use SQL authentication and Azure AD authentication for our SQL databases. The password for the SQL admin gets generated randomly as part of our pipeline and stored in Keyvault. We also have a dedicated team of SQL DBAs who would need to connect to the deployed SQL resources using their Azure AD credentials.
Technically it is possible as per this [link](https://docs.microsoft.com/en-us/azure/templates/microsoft.sql/2019-06-01-preview/servers/administrators) to set an Azure AD group as the SQL admins but I could not find a good example on how to do this with ARM.

You will need 3 things to be able to set an Azure AD SQL admin:

1. The tenantID. This is your Azure AD tenant ID and will need to be passed on to the tenantId property.
2. ObjectID of the group. You can find this in your AzureAD group details and needs to be passed on to the sid property.
3. Name of the group.

![Azure SQL Set Azure AD ADmin]({{ site.url }}/assets/images/2020-06-06-AzureSQL-ADAdmindetails.png)

## End to end ARM template example

If you take the example provided in the link above it's not going to work. You need to specify the SQL server name before `ActiveDirectory`. To do this we use a concat function to concatenate the servername with the ActiveDirectory name like this:

`"name": "[concat(variables('sqlServerName'),'/ActiveDirectory')]"`

Below you can find an end to end solution to deploy a new Azure SQL database and immediately setting an Azure AD group as the SQL admins.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "guidValue": {
      "type": "string",
      "defaultValue": "[newGuid()]"
    },
    "SQLNamePrefix": {
      "type": "string",
      "defaultValue": "[resourceGroup().name]"
    },
    "sqlAdministratorLogin": {
      "type": "string",
      "defaultValue": "SQLAdmin",
      "metadata": {
        "description": "The administrator username of the SQL Server."
      }
    },
    "sqlAdministratorLoginPassword": {
      "type": "securestring",
      "metadata": {
        "description": "The administrator password of the SQL Server."
      }
    },
    "location": {
      "type": "string",
      "defaultValue": "[resourceGroup().location]",
      "metadata": {
        "description": "Location for all resources."
      }
    },
    "LinkedTemplatePrefix": {
      "type": "string"
    }
  },
  "variables": {
    "sqlServerName": "[take(concat('sql-',parameters('SQLNamePrefix'),'-',uniqueString(parameters('guidValue'))),32)]",
    "ADtenantID": "91xxxbe-xxx-43bf-axxx0-c2fxxx47349",
    "ADobjectID": "3exxc5-17xx3-xxb-9axxb2-e1xxx74b76",
    "ADLogin": "Applications Team - Database Administrator"
  },
  "resources": [
    {
      "name": "[variables('sqlServerName')]",
      "type": "Microsoft.Sql/servers",
      "apiVersion": "2019-06-01-preview",
      "location": "[parameters('location')]",
      "tags": {
        "displayName": "SqlServer"
      },
      "properties": {
        "administratorLogin": "[parameters('sqlAdministratorLogin')]",
        "administratorLoginPassword": "[parameters('sqlAdministratorLoginPassword')]",
        "version": "12.0"
      }
    },
    {
      "name": "[concat(variables('sqlServerName'),'/ActiveDirectory')]",
      "type": "Microsoft.Sql/servers/administrators",
      "dependsOn": [
        "[resourceId('Microsoft.Sql/servers', variables('sqlServerName'))]"
      ],
      "apiVersion": "2019-06-01-preview",
      "properties": {
        "administratorType": "ActiveDirectory",
        "login": "[variables('ADLogin')]",
        "sid": "[variables('ADobjectID')]",
        "tenantId": "[variables('ADtenantID')]"
      }
    }
  ],
  "outputs": {
    "sqlServerFqdn": {
      "type": "string",
      "value": "[reference(concat('Microsoft.Sql/servers/', variables('sqlServerName'))).fullyQualifiedDomainName]"
    },
    "sqlServerName": {
      "type": "string",
      "value": "[variables('sqlServerName')]"
    }
  }
}
```

And as you can see, when we deploy a new Azure SQL database the AD admin will be set automatically as part of our template deployment:

![Azure SQL Set Azure AD ADmin]({{ site.url }}/assets/images/2020-06-06-AzureSQL-SetADadmin.png)

Alex
