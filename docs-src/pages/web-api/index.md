---
uid: WebApi.Index
---

[!include[](~/pages/basics/stack/_shared-float-summary.md)]
<style>
  .context-box-summary .browser-interact,
  .context-box-summary .process-apis { visibility: visible; }
</style>


# 2sxc Web API

2sxc has a fully featured WebApi for use in JavaScript or as Headless CMS. So you can call HTTP `GET` to an endpoint like `app/News/data/NewsItems/` and get a list of news items. 


You can also create / modify data using REST, access Queries and work with your custom Web-APIs - across all 2sxc platforms (Dnn / Oqtane / Custom) and with the security you need. 

<img src="./assets/web-api-overview.svg" width="100%">


## Simple Example

Here's an example JavaScript which would run in a 2sxc News-App on a Dnn page:

```javascript
// Get news as a promise
var allNewsPromise = sxc.webApi.get('app/auto/data/News/');

// now log to console
allNewsPromise.then(data => console.log(data));
```

This example has some magic happening in the background. Specifically 3 important things happen on the **client** before sending:

1. The real URL which is requested is a bit longer, but the `webApi` takes care of that.
1. The server needs to know what App and Module the script is calling from. This _Context_ information is also added by the `webApi`.
1. To add security, a crypto-token is added which will prove that the JavaScript requesting this is running on the page. This is also added by `webApi`.

When the **server** receives the request, it too does important stuff.

1. First it will use the URL and _Context_ information to figure out what _Site_, _Language_ and _App_ should be accessed.
1. The server will do some security checks to see if this request should be answered.
1. Then it returns the data in a simple **JSON** format


## Get Started Step 1: Decide which Endpoint you need

This checklist should help you decide:

<iframe src="https://azing.org/2sxc/r/zhLnCg3e?embed=1" width="100%" height="400" frameborder="0" allowfullscreen style="box-shadow: 0 1px 3px rgba(60,64,67,.3), 0 4px 8px 3px rgba(60,64,67,.15)"></iframe>


## Getting Started

Your 1-2-3 steps for using data endpoints are:

1. Decide which endpoint you need
1. Create / Publish the endpoint
   1. For standard endpoints, set the permissions as you need them
   1. For custom endpoints, write the C# code
1. Write the code to read the data (typically in JavaScript)




## Conventions Used 

- [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) means that there is a url convention to access data like `.../blogposts/25`
- [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) also specifies that an _HTTP GET_ is for reading, _HTTP POST_ is for writing, etc.
- All the APIs use [JSON](https://en.wikipedia.org/wiki/JSON) for sending/receiving data. [This is the default schema](https://azing.org/2sxc/r/2zBGrCAd).


## Demo App and further links

You should find some code examples in this demo App
* [REST and WebApi Tutorial](http://2sxc.org/en/apps/app/tutorial-javascript-rest-api-using-jquery-and-angularjs)
* [Razor Web API tutorials](xref:Tut.WebApi)

## Recommended Reading

* [Data CRUD API](xref:WebApi.Data.Index)
* [DotNet WebApi](xref:NetCode.WebApi.Index)
* [Concepts: Polymorphisms](xref:Basics.Polymorphism.Index)

## History

1. Introduced Content-REST API in 2sxc 5.x
1. Query added in 2sxc 8.10
2. Enhanced with Polymorph Editions in 2sxc 9.35 (allowing subfolder/api)
