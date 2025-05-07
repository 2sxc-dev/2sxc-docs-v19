﻿---
uid: ToSic.Eav.DataSources.AttributeFilter
---

The **AttributeFilter** [DataSource](xref:NetCode.DataSources.DataSource) is part of the [Standard EAV Data Sources](xref:Basics.Query.DataSources.Index). It removes values from items so that the result is smaller, and doesn't publish confidential data. It's primarily used when providing data as JSON, so that not all values are published. 

## How to use with the VisualQuery
When using the  [VisualQuery](xref:Basics.Query.VisualQuery.Index)  you can just drag it into your query. Now you can configure what properties you want and not. The following shows a demo which delivers both the data as-is, and also filtered to only deliver `Name` and `Country`:

<img src="./assets/attribute-filter-basic.png" width="100%" class="full-width">

This is what you get on the default-case (unfiltered):

```json
"Default": [
    {
      "Name": "2sic",
      "Country": "Switzerland",
      "Notes": "<p>Secret notes</p>",
      "Categories": [
        {
          "Id": 38646,
          "Title": "Second"
        }
      ],
      "Id": 38653,
      "Guid": "46a46d9e-f572-413c-a42e-a82ac40d929d",
      "Title": "2sic",
      "Modified": "2017-11-06T22:38:00.15Z"
    },
    ...
]
```

This is what you get on the filtered stream:

```json
"Cleaned": [
    {
      "Name": "2sic",
      "Country": "Switzerland",
      "Id": 38653,
      "Guid": "46a46d9e-f572-413c-a42e-a82ac40d929d",
      "Title": "2sic",
      "Modified": "2017-11-06T22:38:00.15Z"
    },
    ...
]
```

As you can see, the secret `Notes` and the `Categories` are not in the _Cleaned_ stream any more. 
There are three common use cases: 

## Programming With The Attribute Filter

[!include["simpler-with-vqd"](shared-use-vqd.md)]

[!include["Read-Also-Section"](shared-read-also.md)]

[!include["Demo-App-Intro"](shared-demo-app.md)]


[!include["Heading-History"](shared-history.md)]
1. Introduced in EAV 3.x, 2sxc ca. v6


[!include["Start-APIs"](shared-api-start.md)]