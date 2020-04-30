---
title: "Saving runtime variables to Azure DevOps Variable Groups"
author: Alexandre Verkinderen
categories:
  - Azure
tags:
  - Azure
  - APIM
---

We use Azure Api Management Service (APIM) quite a lot and recently I have been looking at the new [APIM Developer portal](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-developer-portal) and how to enable Azure Active Directory authentication for the new portal.

## Requirements

To be able to achieve this we will need to manually register a new application in Azure AD. This app will then be used to authenticate against Azure AD from our APIM developer portal. The following list is a list of requirements needed:

- Client ID of new Azure AD application
- Client Secret of new Azure AD application
- Redirect URL of Azure APIM
- Permissions to register new applications in Azure AD

## Add Azure AD identity provider in APIM

First, navigate to your APIM instance, and select **Identities** under the Developer portal settings

:::image type="content" source="../assets/images/2020-05-01-APIM-Addidentity.png" alt-text="Add Identity":::

Click add new identity and select **Azure Active Directory** and copy the **Redirect URL**. We will need this later when we create our Azure AD application.

:::image type="content" source="../assets/images/2020-05-01-APIM-redirecturl.png" alt-text="Redirect URL":::

> [!NOTE]
> Make sure you don't copy the legacy redirect URL if you are using the new APIM portal like me.

Don't close this window just yet. We will need to fill in the ClientID and Client Secret of the new app we are about to register in Azure AD.

## Register a new application in Azure AD

Open a new tab and [register](https://go.microsoft.com/fwlink/?linkid=2083908) a new app in Azure AD. Select **New Registration**. Give your new app a meaningful **name** , select "Accounts in this organizational directory only" and paste the **redirect url** from APIM and press **register**.

:::image type="content" source="../assets/images/2020-05-01-APIM-RegisterAPP.png" alt-text="Register APP in Azure AD":::

Once the app is registered, copy the **ClientID**

:::image type="content" source="../assets/images/2020-05-01-APIM-APPClientID.png" alt-text="ClientID":::

Go to Certificate and Secrets and **create** a new Secret. Once created, copy the Client Secret.

:::image type="content" source="../assets/images/2020-05-01-APIM-APPSecret.png" alt-text="Client Secret":::

There is one last thing we should do in our newly created Azure AD app before switching back to our APIM. Click on **Authentication** and select **ID Tokens**.

:::image type="content" source="../assets/images/2020-05-01-APIM-APPIDTokens.png" alt-text="ID Tokens":::

## Finalize Azure AD identity provider in APIM

Now, let's switch back to our APIM and fill in all the necessary information. Paste the ClientID and Client Secret from the previous step and press **Add**.

:::image type="content" source="../assets/images/2020-05-01-APIM-Appinfo.png" alt-text="Add info":::

At this stage you can already try and login to your APIM with Azure AD. Go to https:yoururl/signin

:::image type="content" source="../assets/images/2020-05-01-APIM-portal-signin.png" alt-text="AD Sign in":::

You will see that the sign in page is using the **Sign-in button: OAuth widget** for Azure AD authentication After sign in the user will be prompted to complete the sign up process.

## Modify the APIM portal for Azure AD authentication

I want all my users to use Azure AD authentication instead of Basic authentication. So I customized the APIM portal and removed all **Basic oAuth widgets** from the portal.

:::image type="content" source="../assets/images/2020-05-01-APIM-portal-RemoveBasic.png" alt-text="Remove Basic oAuth":::

## Conclusion

As you can see it's not complicated to enable Azure AD for the APIM portal. Using Azure AD also means I can now use all the security features in Azure AD like conditional access and MFA for my developers.

Alex