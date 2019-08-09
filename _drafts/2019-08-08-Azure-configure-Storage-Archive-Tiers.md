---
title: "Azure Configure Storage Archive Tier"
categories:
  - Azure
tags:
  - Azure
  - Storage Account
---

Lately I had to setup Azure Archive storage for one of my customers. Azure Archive Storage was launched in 2017 and recently Microsoft announced a 50% price discount in some regions. Setting up Archive storage is really easy but there are few things you need to know or keep in mind especially from a pricing point of view.

## Intro
Azure Archive storage provides a very cheap way to keep a lot of data for a very long time. This tier is intended for data that can tolerate several hours of retrieval latency and will remain in the archive tier for at least 180 days. This means that while data is in the archive tier it is offline and cannot be modified or read. The blob metadata remains online which is how you query and list the data in the archive storage. For blobs (or data files) in archive, the only valid operations are GetBlobProperties, GetBlobMetadata, ListBlobs, SetBlobTier, and DeleteBlob.

To read or modify data in an archive storage, you must change the tier of the blob from archive to hot or cool. This is called "blob rehydration" and can take up to 15 hours!

## Pricing
Now this is where things get interesting :-)
As said above, Archive storage is to keep a lot of data for a very long time without accessing that data. Storing data is super cheap but retrieving data is super expensive.
![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/2019-08-08_Storage_Pricing.png)

As you can see the read operations are going to be really expensive if you need to retrieve something from Azure Archive.
And it gets even more interesting if you are moving data between tiers. When data is moved to a cooler tier (hot -> cool -> archive) the operation is billed as write operation. When data is moved to a hotter tier (Archive -> cool -> hot) data is billed as a read operation.

And last but not least. You also pay an early deletion fee if you move data between tiers before the "cool early deletion period" you will pay an early deletion fee. The cool tier has a "cool early deletion period" of 30 days and the archive tier has a "cool early deletion period" of 180 days. So if you move data to the arhive tier and retrieve it after 50 days you will be charged an early deletion fee equivalent to 130 days (180 days minus 50 days).

### Pricing Example
Let's do a quick calculation for the following scenario:
One off 50TB stored for 10 years in a hot tier vs archive tier:


Now let's assume we need to retrieve the archived data after 5 years for an audit and move it to the hot tier:

## Storage LifeCycle Management
Storage LifeCycle management lets you move data between tiers automatically to optimize for performance and costs. When defining the lifecycle management keep the early deletion fee in mind :-) . Go to your storage account, LifeCycle Management and define your rules

![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/2019-08-08_storage_lifecycle_,management.png)

Defining a filter set is not mandatory. So this rule will move data from hot to cool storage after 30 days after blob last modification. Move to archive storage after 90 days after blob last modification and delete 3650 days (or 10 years) after blob last modification.


### Conclusion

And that's a wrap, yo! You survived the tumultuous waters of alignment. Image alignment achievement unlocked!
