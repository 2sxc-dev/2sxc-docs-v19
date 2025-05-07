---
uid: ToSic.Eav.DataSources.PublishingFilter
---

The **PublishingFilter** [DataSource](xref:NetCode.DataSources.DataSource) is part of the [Standard EAV Data Sources](xref:Basics.Query.DataSources.Index). It will hide unpublished items for non-editors and provide these drafts if an editor is viewing the results.  

## How to use with the VisualQuery
When using the  [VisualQuery](xref:Basics.Query.VisualQuery.Index)  you can just drag it into your query. Here's a picture showing app data with or without publishing filter:  

<img src="./assets/app-compare-no-in-with-publishing-filter.png" width="100%" class="full-width">

## Configuring the PublishingFilter DataSource
The PublishingFilter has no configuration. 

## How does it work?
Since the published/unpublished is a very common query, internally the cache actually already provides different streams for this - and the PublishingFilter simply chooses the stream based on the current permissions. 


## Programming With The PublishingDataSource
[!include["simpler-with-vqd"](shared-use-vqd.md)]

[!include["Read-Also-Section"](shared-read-also.md)]

[!include["Demo-App-Intro"](shared-demo-app.md)]

[!include["Heading-History"](shared-history.md)]

1. Introduced in EAV 3.x, in 2sxc ?


[!include["Start-APIs"](shared-api-start.md)]