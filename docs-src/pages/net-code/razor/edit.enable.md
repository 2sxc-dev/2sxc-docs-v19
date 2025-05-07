---
uid: NetCode.Razor.Edit.Enable
---
# @Edit.Enable Method in C# Razor (Deprecated)

> [!WARNING]
> This is deprecated but will continue to work for a very long time. 
> For anything new, see [](xref:JsCode.2sxcApi.Activate.Index)

Editing or adding data to a 2sxc app requires the UI to have some JS, CSS and context information. This is only loaded/included for editors/admin/super-users, and not available for users with limited permissions.

If you want to enable this for more restricted users - for example when you want to use the 2sxc-form to let users add data - this must be enabled. That's what `Edit.Enable(...)` is for.


[!include["Razor Tutorials"](~/shared/tutorials/razor.md)]


## How to use

This example shows how you enable the UI using Razor, which will allow public users to create data:

```razor
<div>
    @Edit.Enable(api: true, forms: true, context: true, autoToolbar: false)
</div>
```

This example ensures that

1. `api`: basic JS for editing are loaded, allowing you to then run javascript commands like `$2sxc(...).run(...)`
1. `forms`: additional JS is loaded, enabling the standard form dialogs to open
1. `context`: the html contains context-information about the app, so that the dialogs actually work - see also [edit context](xref:Basics.Browser.EditUx.EditContext)
1. the auto-toolbars are disabled (this would generate a default toolbar if no toolbar was specified)

## Usage Notes

This command simply enables editing - but doesn't provide any permissions or show any buttons yet. Here are a few things you must know to get this to work:

1. remember to set [permissions](xref:Basics.Cms.Permissions.Index) to allow what you want to do (like create new draft items for public users)
1. Edit.Enable uses [named parameters](xref:NetCode.Conventions.NamedParameters), so you always have to use the `api: true` syntax
1. the Edit.Enable won't output anything in the position it's added, because it controls the main wrapper
1. you must also create a link or toolbar in your code for the public users, as they won't have a button to press otherwise


## Read also

* [Tutorial app for Public Forms](https://2sxc.org/en/apps/app/tutorial-public-forms-with-2sxc-9-30)
* [Blog Recipe for using Public Forms with 2sxc](https://2sxc.org/en/blog/post/recipe-create-public-forms-with-2sxc)


## History

1. Introduced in 2sxc 9.30

