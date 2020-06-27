---
title: "The curious case of an Azure Application Gateway showing no metrics and logs"
categories:
  - Azure
tags:
  - Azure
  - Azure Application Gateway
header:
  og_image: /assets/images/2020-06-24-Azureappgw-nometrics.png
---

This is the curious story of an Azure Application Gateway showing no metrics and logs at all. Even thought this was one the main customer's production Application Gateways we could see 0 requests in the metrics. These metrics should show up regardless if you have log analytics configured or not.

![App gateway no metrics]({{ site.url }}/assets/images/2020-06-24-Azureappgw-nometrics.png)

Our diagnostic logs are automatically configured based on this [Azure Policy written by Tao](https://blog.tyang.org/2019/05/19/deploying-azure-policy-definitions-via-azure-devops-part-1/). We double checked the diagnostics settings were enabled, which was the case, but still no logs were stored in Log Analytics:

![App gateway no metrics]({{ site.url }}/assets/images/2020-06-24-Azureappgw-nologs.png)

## Issue

I logged a ticket and the Azure support team came back after a few days saying that the issue is due to some [custom SSL Policy](https://docs.microsoft.com/en-us/azure/application-gateway/application-gateway-ssl-policy-overview) on the Azure Application Gateway. The customer did change the default SSL settings and was using the following custom SSL settings:

```json
 "SSLPolicy": {
            "CipherSuites": [
                "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256",
                "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384",
                "TLS_RSA_WITH_AES_128_GCM_SHA256"
            ],
```

![App gateway no metrics]({{ site.url }}/assets/images/2020-06-24-Azureappgw-CustomSSL.png)

## Solution

In order to make the logs and metrics work, we had to add 2 more cypher suites :

- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256

The reason for this is that the Azure Application Gateway V1 writes logs to a storage account in the backend. This storage account requires certain cypher Suites to be enabled in order to be able to store the logs and metrics to that storage account. The following 3 cypher suites below must be enabled:

- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256

So make sure you have at least the 3 cypher suites mentioned above as seen in the picture.

![App gateway no metrics]({{ site.url }}/assets/images/2020-06-24-Azureappgw-fixSSL.png)

## Conclusion

Don't mess with the SSL settings :smiley:.

A few seconds after adding the 2 missing cypher suites the metrics and logs started to show up.

![App gateway no metrics]({{ site.url }}/assets/images/2020-06-24-Azureappgw-metrics.png)

Hope this helps,

Alex
