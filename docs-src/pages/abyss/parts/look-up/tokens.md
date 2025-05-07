---
uid: Abyss.Parts.LookUp.Tokens
---

[!include[](~/assets/features/look-up-system.md)]

# LookUp Tokens Explained

[!include[](~/pages/basics/stack/_shared-float-summary.md)]
<style>.context-box-summary .query-params, .context-box-summary .lookup { visibility: visible; } </style>

Often you need a _placeholder_ which should be resolved at runtime with a real value from elsewhere.

In Dnn / 2sxc this is called a **Token**, and they usually look like `[Source:Property]`.

## Simple Example

As example could be `[DateTime:Now]` which would be resolved to the current date/time at runtime.
You would use this in a [Query](xref:Basics.Query.Index) to filter out news which should be published in future, so `PublicationDate < [DateTime:Now]`.

> [!NOTE]
> There is also a [TokenEngine](xref:ToSic.Sxc.Engines.TokenEngine) which uses the same Token mechanism to generate HTML. What you see here also applies to that, but it's actually a separate topic.


## Some Token Examples

1. `[Portal:PortalId]` would return the current portal Id
1. `[App:Settings:PageSize]` would return the page size as configured in app-settings
1. `[QueryString:Id]` would retrieve the id-parameter from the url
1. `[MyConfiguration:ProductId]` would retrieve the id as configured in the UI by the user
1. `[MyConfiguration:productId||27]` would also try to get the id, but return 27 if not found



## Token Basics

A token is a piece of text that looks like `[Source:Property]`, which will be replaced by an engine so that it will then be a value. For example, `[QueryString:Page]` is replaced with `2` if the current url has `?page=2` in it. You can research more about tokens [in older docs here](https://2sxc.org/en/Learn/Token-Templates-and-Views) and in the [full list of standard tokens](https://2sxc.org/dnn-app-demos/en/Apps/Tutorial-Tokens), it's a standard Dnn concept.

Internally it uses a LookUp-Engine which itself uses LookUp-Sources - see [](Abyss.Parts.LookUp.Index.

## Special Token Features in 2sxc/EAV

The EAV and 2sxc have enhanced Tokens to a new level with these features:

### 1. Sub-Tokens

A token like `[App:Settings:PageSize]` will go through a tree of info-objects to find an inner property if it exists. This only works on special object types that are specifically meant to provide sub-data.

### 2. Fallback

A token like `[QueryString:page||1]` will deliver the url-param, and if that is empty, will deliver `1`. Note that you need 2 pipe symbols `|` because the convention is that after the first pipe you can have a format specifier like `#.##`.

### 3. Stacking

Stacking with more Tokens: a token like `[QueryString:PageSize||[App:Settings:PageSize]]` will try the first token, and if it doesn't resolve, try the next one

### 4. Recursion

A token can resolve into a token, which would then be looked up again. So if a token `[MyConfiguration:Page||1]` is used, and the setting `Page` is not a number but again a token like `[QueryString:Page]`, then it will...

1. resolve `Settings:Page` and find `Querystring:Page`
1. resolve `QueryString:Page` and maybe find something
1. if that is empty, return the fallback 1


## Advanced Token Sources in Special Scenarios

Some situations will have token sources beyond the default. For example, when configuring data sources they always have 2 more sources

* `In` - used like `[In:Default:PageSize]`
* `MyConfiguration` - used like `[MyConfiguration:PageSize]`
* There is another special [override-token system](xref:Basics.Query.Parameters.TestParameters) which is used for testing

## Also Read

* [](xref:Abyss.Parts.LookUp.Index)
* [](xref:ToSic.Eav.DataSource.IDataStream)
* [](xref:NetCode.DataSources.Custom.Guide.BigPicture)
* [](xref:NetCode.DataSources.Custom.ConfigurationParse)


## History

1. General Tokens introduced in 2sxc 1.0
1. Most enhancements were in 2sxc 07.00
