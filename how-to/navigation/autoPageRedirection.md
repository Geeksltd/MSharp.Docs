# Auto Page Redirection

## Problem

As soon as the user navigates to a page, you want that page to redirect the user to somewhere else.

An example would be when an Admin user wants to access the Settings section, which automatically redirects them to the Administrators page.

## Implementation

With MSharp, you can update the page to navigate to a different page, as part of `OnStart()`.

```csharp
public class SettingsPage : SubPage<AdminPage>
{
    public SettingsPage()
    {
        Set(PageSettings.LeftMenu, "AdminSettingsMenu");

        OnStart(x => x.Go<Settings.AdministratorsPage>().RunServerSide());
    }
}
```
