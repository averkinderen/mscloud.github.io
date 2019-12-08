---
title: "Securing your Azure Functions App with API Management"
categories:
  - Azure
  - Functions App
tags:
  - Azure
  - Azure Functions App
  - Azure API Management
  - Azure Security
---

This article will show you how to use an Azure Managed Identity to authenticate against an Azure Functions app that is exposed through Azure API Management.

We will assume you already have an Azure Function App up and running. If not, have a look [here](https://docs.microsoft.com/bs-latn-ba/azure/azure-functions/functions-openapi-definition). This example will walk you through the creation of an Azure Functions App and expose that Function with Azure API management.

Once we have our Azure Functions App up and running we need to secure it. By default it is exposed to the world wide web. There are a few things you can do to secure your Functions App like:

* Enabling Azure AD authentication
* IP Whitelisting

In this article we will discuss Azure AD authentication with Managed Identities. When we enable Azure AD authentication on our Functions App we need to find a way for our Azure API Management (APIM) to authenticate as well.
This is where Managed Identities comes into the picture. A system-assigned Managed Identity is enabled directly on the Azure resource. When the identity is enabled, Azure creates an identity for the instance in the Azure AD tenant. After the identity is created, the credentials are provisioned onto the instance. The lifecycle of a system-assigned identity is directly tied to the Azure resource that it's enabled on. If the resource is deleted, Azure automatically cleans up the credentials and the identity in Azure AD.

So, no need to save passwords, no need to rotate credentials etc. Everything is done automatically for your in the background.

## Enabling Managed Identity on Azure APIM

Enabling a Managed Identity is super easy. Go to the resource, Settings, Managed Identity and click On.

![Enabling Managed Identity]({{ site.url }}/assets/images/2019-12-08-APIM-ManagedIdentity.png)

This can also be done on creation of the resource as part of your ARM template:

```Json
      "identity": {
        "type": "SystemAssigned"
      }

```

Once the Managed Identity is created, go to AAD and grab the objectID. We will need it later.

![APIM ObjectID]({{ site.url }}/assets/images/2019-12-08-APIM-ObjectID.png)

## Enabling AAD authentication in Azure Functions

We can now go ahead and enable Azure AD authentication on our Functions App.

![Functions Enable AAD]({{ site.url }}/assets/images/2019-12-08-FunctionsApp-EnableAAD.png)

Select Azure Active Directory as the authentication provider:

![Functions APP Settings]({{ site.url }}/assets/images/2019-12-08-FunctionsApp-AADsettings.png)

For the purpose of this blog post we will use Express Settings:

![Functions AAD APP]({{ site.url }}/assets/images/2019-12-08-FunctionsApp-AADAP.png)

We will now get an unauthorized error when we try to call our Functions APP:

![Functions AAD Unauthorized.]({{ site.url }}/assets/images/2019-12-08-APIM-Unauthorized.png)

This is expected as the APIM does not have a bearer token to authenticate against the Functions App.

## Change APIM authentication policy to use the Managed Identity

For the APIM to authenticate against AAD and receive a bearer token we need to change the APIM Inbound Policy. We will use the authentication-managed-identity policy to authenticate with our Azure Functions APP using the managed identity of the APIM. This policy uses the managed identity to obtain an access token from AAD for accessing the specified resource. After successfully obtaining the token, the policy will set the value of the token in the Authorization header using the Bearer scheme.

```XML
    <inbound>
        <base />
        <authentication-managed-identity resource="OBJECTID of the Managed Identity" ignore-error="false" />
        <set-header name="Ocp-Apim-Subscription-Key" exists-action="delete" />
    </inbound>
```

Let's give it a try now and call our API:

![APIM Success]({{ site.url }}/assets/images/2019-12-08-APIM-Success.png)

When we look in the trace logs we can see that the APIM Policy will authenticate against Azure AD, receive a bearer token and authenticate against the Azure Functions App:

![APIM token]({{ site.url }}/assets/images/2019-12-08-APIM-MI-Authentication.png)

## Conclusion

Managed Identities can be used for that last Password less authentication against your backed services. I want to thank [Toon Vanhoutte](https://toonvanhoutte.wordpress.com/) to help me out when I got stuck.

Alex