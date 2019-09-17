---
title: "Configure Azure Storage Archive Tier"
categories:
  - Azure
tags:
  - Azure
  - Storage Account
---

Lately I had to setup Azure Archive storage for one of my customers. Azure Archive Storage was launched in 2017 and recently [Microsoft announced a 50% price discount](https://azure.microsoft.com/en-au/blog/we-re-making-azure-archive-storage-better-with-new-lower-pricing/) in some regions. Setting up Archive storage is really easy but there are few things you need to know or keep in mind especially from a pricing point of view.

## Intro

Azure Archive storage provides a very cheap way to keep a lot of data for a very long time. This tier is intended for data that can tolerate several hours of retrieval latency and will remain in the archive tier for at least 180 days. This means that while data is in the archive tier it is offline and cannot be modified or read. The blob metadata remains online which is how you query and list the data in the archive storage. For blobs (or data files) in archive, the only valid operations are GetBlobProperties, GetBlobMetadata, ListBlobs, SetBlobTier, and DeleteBlob.

To read or modify data in an archive storage, you must change the tier of the blob from archive to hot or cool. This is called "blob rehydration" and can take up to 15 hours!

## Pricing

Now this is where things get interesting :-)
As said above, Archive storage is to keep a lot of data for a very long time without accessing that data. Storing data is super cheap but retrieving data is super expensive.
![pricing]({{ site.url }}/assets/images/2019-08-08_Storage_Pricing.png)

As you can see the read operations are going to be really expensive if you need to retrieve something from Azure Archive.
And it gets even more interesting if you are moving data between tiers. When data is moved to a cooler tier (hot -> cool -> archive) the operation is billed as a write operation. When data is moved to a hotter tier (Archive -> cool -> hot) data is billed as a read operation. The process of moving blobs out of the Archive tier is called "rehydration". By default it will take up to 15 hours but now in [public preview Microsoft released priority retrieval](https://azure.microsoft.com/en-us/blog/azure-archive-storage-expanded-capabilities-faster-simpler-better/ ) where you can retrieve blobs under 10GB in less than an hour.

And last but not least. You also pay an early deletion fee if you move data between tiers before the "cool early deletion period" you will pay an early deletion fee. The cool tier has a "cool early deletion period" of 30 days and the archive tier has a "cool early deletion period" of 180 days. So if you move data to the archive tier and retrieve it after 50 days you will be charged an early deletion fee equivalent to 130 days (180 days minus 50 days).

### Pricing Example

Let's do a quick calculation for the following scenario:
One off 50TB stored for 10 years in a hot tier vs archive tier:

![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/2019-09-11_11-42-21-pricing.png)
As you can see the monthly estimated cost of having 50TB in the hot tier is $1,025 or $123,000 for 10 years. The monthly cost for Archive storage is $260 a month or $31,000 for 10 years.

Now let's assume we need to retrieve the 50TB archived data after 10 years for an audit and move it to the hot tier:
![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/2019-09-11_11-48-03-archiveretrieval.png)
As you can see for that one particular month where we need to retrieve the data for an audit we will get a bill of $5000 but overal, on the long term, archive storage is still going to be a lot cheaper.

## Storage LifeCycle Management

Storage LifeCycle management lets you move data between tiers automatically to optimize for performance and costs. When defining the lifecycle management keep the early deletion fee in mind :-) . Go to your storage account, LifeCycle Management and define your rules

![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/2019-08-08_storage_lifecycle_,management.png)

Defining a filter set is not mandatory. So this rule will move data from hot to cool storage if the blob file hasn't been modified for 30 days. It will move the blog to archive storage if the blob hasn't been modified for 90 days and delete hte blob after 3650 days (or 10 years).

## Conclusion

Archive storage together with Storage LifeCycle Management is one of those hidden gems that not a lot of customers are using but for data that is not being accessed often it can save a lot of money.

And that's a wrap!
