# Page Role Inheritance

## Problem

You want to limit who has access to sections of an application based on a given role, without having to handle the access on each individual page.

For example, only Admin users should have access to all pages that are part of the Settings section.

## Implementation

With MSharp, you can add Roles to the pages.

Whilst they can be applied on every page, you can instead apply them to just the root/parent pages in question.

Using the above example, you can simply apply the Roles for just the Settings page:

```csharp
public class SettingsPage : SubPage<HomePage>
{
    public SettingsPage()
    {
        Roles(AppRole.Admin);

        Set(PageSettings.LeftMenu, "AdminSettingsMenu");

        OnStart(x => x.Go<Settings.GeneralPage>().RunServerSide());
    }
}
```

This way, not only will the Settings page be restricted to Admin users, but it also means that all sub pages of Settings will by default be restricted to Admin users as well.

So even if no Roles were defined for the General page:

```csharp
public class GeneralPage : SubPage<SettingsPage>
{
    public GeneralPage()
    {
        Add<Modules.GeneralSettingsForm>();
    }
}
```

Because it is a sub page of Settings, it will by default still restrict the page to Admin users only.
