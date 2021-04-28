# Custom Page Url

## Problem

By default, the url of a page is based on both the page hierarchy and the name of the page in question.

However, there may be a scenario where you want a page's url to be different from the default used.

For example, you have an application that has a page in Admin for handling general settings, with the following url:

> <http://examplesite.com/admin/settings/general>

However, you want the url for that page to be changed, whilst still retaining the name of the page itself.

## Implementation

With MSharp, you can set the `Route()` of the page to achieve this.

For example, the following will set the page's url to:

> <http://examplesite.com/admin/settings/general-settings>

```csharp
public class GeneralPage : SubPage<SettingsPage>
{
    public GeneralPage()
    {
        Route("admin/settings/general-settings");
        Add<Modules.GeneralSettingsForm>();
    }
}
```

> **Note**: When setting the route, make sure that the custom url you want is not already being used by another page in the application.
>
> Also, depending where in the page hierarchy you are defining the custom url, what you provide for `Route()` can end up providing a different url than intended.
>
> Using the above example, if the `Route()` was instead set to just the following:
>
> ```csharp
>   Route("general-settings");
> ```
>
> Then it would produce the following url:
> > <http://examplesite.com/general-settings>
>
