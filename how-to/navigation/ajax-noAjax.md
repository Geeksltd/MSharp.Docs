# Ajax/no ajax

## Problem

M# application is powered by Ajax-based navigation to bring the SPA experience. You want to know related pieces in play and how to enable or disable this feature on the various levels like master page, module or a single button.

## Motivation
Web technologies like HTML and HTTP originally were created for sharing documents without user experience in mind. We can’t get a new Web redesigned from the foundation up and break the existing systems. Improvements like interactivity and user experience have been added later to the existing foundation. Ajax was one of the technologies created for providing a continuous feel, flicker-free updates, interface facilities, live data and so on.

Traditional web and ASP.Net is based on a request/response model that for each request all the content files like HTML, javascript, CSS, images will be sent to the browser. That is inefficient, slow and affects user experience. Single-page applications (SPA) emerged as a solution to this problem.

M# uses jQuery Ajax internally in the Olive framework to bring the SPA experience. It replaces only the main content in the master page for each request by changing traditional navigation with ajax requests and hijacking the click events in the javascript engine.

## Generated Markup
An attribute named `data-redirect` added to the markup for marking links in the page for javascript engine to hijack them for ajax navigation.
```html
<a href="/admin/settings/administrators" data-redirect="ajax">Administrators</a>
```

## Project level
Ajax navigation is enabled at the project level by using `AjaxRedirect` method for the master page in the project definition:

```csharp
public class Project : MSharp.Project
{
    public Project()
    {
        //...
        Layout("Admin default")
            .AjaxRedirect()
            .Default()
            .VirtualPath("~/Views/Layouts/AdminDefault.cshtml");
        Layout("Login")
            .AjaxRedirect()
            .VirtualPath("~/Views/Layouts/Login.cshtml");
    }
}
```
Also, in template file **AdminDefault.cshtml** layout refresh is disabled for ajax navigation.
```html
@{Layout = Request.IsAjaxCall() ? null : "~/Views/Layouts/AdminDefault.Container.cshtml";}
<main>
    <!-- ... -->
</main>
```

## Module level
In case you're using a third-party Javascript library and behaving strangely and you suspect it might not be compatible with Ajax navigation, then on the module that is using that library use `AjaxRedirect` method with `false` argument.

```csharp
public ContactsList : ListModule<Domain.Contact>
{
    public ContactsList()
    {
        AjaxRedirect(false);
        //...
    }
}
```
or similarly, in the menu you can use ths method:
```csharp
public class MainMenu : MenuModule
{
    public MainMenu()
    {
        AjaxRedirect(false);
        //...
    }
}
```

## Button level
You can disable ajax on button level to change its navigation with a full page refresh.

```csharp
public ContactsList : ListModule<Domain.Contact>
{
    public ContactsList()
    {
        //...
        Button("New Contact")
            .UseAjaxGetMethod(false)
            .OnClick(x => x.Go<Contact.EnterPage>().SendReturnUrl());
    }
}
```