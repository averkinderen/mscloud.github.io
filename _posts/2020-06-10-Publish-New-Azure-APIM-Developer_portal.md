---
title: "Publish the new Azure API Management Service Developer Portal behind an Application Gateway"
categories:
  - Azure
tags:
  - Azure
  - Azure APIM
header:
  og_image: /assets/images/2020-06-06-AzureSQL-SetADadmin.png
---

There are currently 2 developer portals for the Azure API Management service: a legacy portal and the [new portal experience](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-developer-portal). We deployed our Azure APIM instance before the new portal was released so we were still running on the legacy portal. We are running our Azure APIM instance with custom domains on an internal vnet behind an application gateway with WAF and the default OWASP 3.0 rules enabled. This appeared to be a real challenge with the new developer portal.

In this blogpost I will cover how to move to the new developer portal experience and changes that are required on your Application Gateway.

## 1) Create new custom domain for the new APIM Management Endpoint

If we want to use the new developer portal we need to publish a new APIM management endpoint and create a new CNAME in our publis DNS register. The old developer portal only requires the portal endpoint to be published as shown below:

![Custom domains]({{ site.url }}/assets/images/2020-06-10-AzureAPI-Customportal.png)

To add the new management endpoint click **custom domains** and **add new**. Select **Management** and provide your custom hostname and certificate.

![add management point]({{ site.url }}/assets/images/2020-06-10-AzureAPI-mpendpoint.png)

## 2) Remove the Legacy developer portal custom domains and add the new developer portal domain

Next, we will add the new developer portal with a custom domain and remove the legacy developer portal custom domain. Your custom domains should look like this:

![remove legacy portal]({{ site.url }}/assets/images/2020-06-10-AzureAPI-removelegacyportal.png)

## 3) Update WAF rules on Azure Application Gateway

I have my Azure APIM sitting on a [virtual network behind an Azure Application gateway](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-integrate-internal-vnet-appgateway#--scenario). The legacy portal is fully comptabile with WAF OWASP 3.0 rules. However, as of writing this article, the new Azure APIM developer portal is not fully compatible with the industry standard OWASP rules. The WAF will block certain requests and treat them as SQL injections for example. Luckily my WAF and App gateway are only used for this APIM so I could lower my security, as a workaround, and disable certain rules. But I can imagine you would not be so happy to disable those rules if all your traffic is going through the same app gateway. The following rules are to be disabled:

- Rule 920311: Missing User Agent Header
- Rule 931130: Possible Remote File Inclusion (RFI) Attack: Off-Domain Reference/Link
- Rule 942100: SQL Injection Attack Detected via lib injection
- Rule 942110: SQL Injection Attack: Common Injection Testing Detected
- Rule 942200: Detects MySQL comment-/space-obfuscated injections and backtick termination
- Rule 942430: Restricted SQL Character Anomaly Detection (args): # of special characters exceeded (12)
- Rule 942440: SQL Comment Sequence Detected

![WAF Rules]({{ site.url }}/assets/images/2020-06-10-AzureAPI-WAFRules.png)

## 4) Update Azure Application Gateway Routing Rules and Health Probe

Next, as we have a new endpoint, we need to update our health probes and app gateway settings. Go to your Azure Application Gateway and configure the listener and rules like this:

**Create a new Health Probe**

Add the new management endpoint public address the host.

![Health probe]({{ site.url }}/assets/images/2020-06-10-AzureAPI-addHealthProbe.png)

Notice that we used `/servicestatus` for the path.

**Create new HTTP Settings**:

Add the following new HTTP setting to include the new management endpoint:

![http setting]({{ site.url }}/assets/images/2020-06-10-AzureAPI-addHTTPSetting.png)

**You will need to add 2 new listeners**:

You wil need to create 2 listeners. One for the management endpoint on http and one for https:

![listener https]({{ site.url }}/assets/images/2020-06-10-AzureAPI-ListenerhttpsManagement.png)

**You will also need to add 2 new routing rules**:

Create 2 new routing rules for http and https:

![add https routing rule]({{ site.url }}/assets/images/2020-06-10-AzureAPI-addroutingrulehttps.png)

![add http routing rule]({{ site.url }}/assets/images/2020-06-10-AzureAPI-addroutingrule.png)

That's it for the application gateway.

## Reprovision the new Developer portal

The new developer portal was not provisioned correctly in my environment. I had a blank screen when I checked if it was working properly. After logging a call with MS support they told me I had to reprovision the new developer portal. I guess that's due to the WAF rules blocking certain requests and the new portal was not properly provisioned. To provision the new portal you will need a script that you can [find here](https://github.com/averkinderen/APIM/tree/master/ProvisioningNewPortal). It will require [node js](https://nodejs.org/dist/v12.16.1/node-v12.16.1-x64.msi) to be installed.

For the script to execute you need a management API key. Go to your API management instance and in ‘Management API ‘ click  **enable** and **generate** to get the Shared access signature token.

![SAS key]({{ site.url }}/assets/images/2020-06-10-AzureAPI-APImanagement.png)

Open the `generate-data.bat` file and fill in your shared access key and update the management endpoint:

![generate data]({{ site.url }}/assets/images/2020-06-10-AzureAPI-generate-data.png)

Run the bat file from the command prompt. This will provision the new API developer portal experience.

Hope this helps,

Alex
