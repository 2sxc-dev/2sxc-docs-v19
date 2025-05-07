---
uid: JsCode.Toolbars.Old
---

<img src="~/assets/features/toolbar.svg" class="feature">

# Old APIs for In-Page Edit Toolbars and Buttons

[!include[](~/pages/basics/stack/_shared-float-summary.md)]
<style>.context-box-summary .edit-custom { visibility: visible; } </style>

> [!WARNING]
> These are old APIs and fairly complicated. 
> We suggest you don't use them any more!

## How to Use v9.40 (old, not recommended)

The most common use-case is actually to provide some HTML, which the JavaScript will pick up automatically and convert into a menu. The syntax was revised in 2sxc 9.40+, which is what we show here. The previous syntax is still supported, but not recommended any more:



```HTML
<!-- this is the default toolbar for first content item assigned to this module -->
<div sxc-toolbar='{
    "toolbar": {"sortOrder":0,"useModuleList":true}
}'>
</div>


<!-- this is a toolbar for a content-item with the id 6875 -->
<div sxc-toolbar='{
    "toolbar": {"entityId":6875}
}'>
</div>


<!-- this could be a custom toolbar for showing a new-button only -->
<div sxc-toolbar='{
    "toolbar": {"contentType":"BlogPost","action":"new"}
}'>
</div>


<!-- this would have two buttons, each configured in a way --> 
<div sxc-toolbar='{
    "toolbar": [{
        "action":"edit",
        "useModuleList":true,
        "sortOrder": 0,
        "prefill": { "DocumentedOnPage": "page:@Dnn.Tab.TabID", "title": "@Dnn.Tab.Title" }
    }, {
        "action" : "new",
        "contentType" : "BlogPost"
    }]
}'>
</div>
```

## What was Changed/Enhanced in 2sxc 9.40

There were some things which worked well, but bothered us as perfectionists :). It boils down to how much of the page html must be different just because editing is used. So this is what we wanted to change:

1. the previous implementation always used a special class `sc-element` to mark the tag which detects mouse-over. This was necessary, because the tag itself was added in another place in the code. This is not necessary any more, since the `sxc-toolbar` attribute is now on the tag which does the hover-detect.

1. the previous implementation created a `<ul>` tag in the source code. Though this was not a big issue, it just didn't feel right.

1. the previous implementation spread the information for the toolbar on two attributes `toolbar` and `settings` - this just wasn't perfect. Now it's both in the `sxc-toolbar` attribute.

## How to Use before 2sxc 9.40

```HTML
<!-- this is the default toolbar for content assigned to this module -->
<ul class="sc-menu" toolbar='{"sortOrder":0,"useModuleList":true,"isPublished":true}'></ul>

<!-- this is a default toolbar for content-items not assigned to this module -->
<ul class="sc-menu" toolbar='{"isPublished":true,"entityId":6875}'></ul>

<!-- this could be a custom toolbar for showing a new-button only -->
<ul class="sc-menu" toolbar='{"contentType":"BlogPost","action":"new"}'></ul>

<!-- this would have two buttons, each configured in a way --> 
<ul class='sc-menu' toolbar='[{
    "action":"edit", 
    "useModuleList":true, 
    "sortOrder": 0, 
    "prefill": { "DocumentedOnPage": "page:@Dnn.Tab.TabID", "title": "@Dnn.Tab.Title" } 
}, {
    "action" : "new",
    "contentType" : "BlogPost" 
}]'></ul>
```

## How it Works

Internally, a lot will happen to actually turn that into a real, usually floating, toolbar. Basically what happens is

1. a script picks up all cases of `<* sxc-toolbar=...>` and `<ul class="sc-menu ..."></ul>`
2. it will then pass it to a toolbar creator which will either create a standard-list of buttons, or a custom one
3. the resulting buttons/links will be placed in `<li>` items and added to the `<ul>` tag

But you could also do a whole lot more, including custom buttons and code (since 2sxc 08.06)

```html
<div sxc-toolbar='{ "toolbar": {
    "groups": [
        {
            "name": "my default list",
            "buttons": "edit,add,more"
        },
        {
            "name": "list buttons",
            "buttons: "sort,moveup,movedown,more"
        },
        {
            "name": "really advanced stuff",
            "buttons": [
                "app",
                "zone",
                {
                    "command":{
                        "action": "custom",
                        "customCode": "alert(&apos;hello&apos;)"
                    }
                    "icon": "icon-sxc-bomb"
                },
                "more"
            ]
        }
    ],
    "defaults": {
        "entityId": 740,
        "contentType": "BlogPost"
    }
}}'>
...
</div>
```

All the configuration is in the `sxc-toolbar` attribute, which contains two main nodes:

1. `toolbar` - see below
2. `settings` - see [Toolbar Settings](xref:JsCode.Toolbars.Settings)

In the old syntax (before 2sxc 9.40, using the `<ul>` tag, two attributes are handled
1. `toolbar` or `data-toolbar` - see below
2. `settings` or `data-settings` - see [Toolbar Settings](xref:JsCode.Toolbars.Settings)


## More Background
The `toolbar` information is:

1. an object with some properties (like `entityId`) and _no_ `action` verbs --> then it will auto-generate all default buttons  
`{ entityId: 17, isPublished: true }`

1. an object with some properties and 1 or more action verbs --> generate only these buttons  
`{ actions: "new,edit", useModuleList: true, sortOrder: 1 }`

1. an array with commands (objects with 1 verb) --> generate these Buttons  
`[{ action: ...}, { action: ...}]`

1. on object containing a buton-group like  
`{ buttons: [ { command: { action: ...}}, { command: ...}] }`

1. a group of button-groups  
`[ { buttons: ... }, {buttons: ...}]`

1. a full toolbar configuration  
`{ groups: [...], defaults: {...}, params: {...} }`


For a full scope of what is possible, you should read the [js toolbar documentation](xref:JsCode.Toolbars.Advanced).

## Demo App and further links
* [JS Manage / Toolbar API Tutorial App](http://2sxc.org/en/apps/app/tutorial-for-the-javascript-apis-and-custom-toolbars)

## History
1. Introduced in 2sxc v02.00
2. Published API for use in templates in 2sxc v08.06
3. Enhanced / Standardized in 2sxc v09.40