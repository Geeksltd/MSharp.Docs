# Main navigation menu

## Problem

You want to have a menu that is shown for all users when they are logged in to the website to show the visual representation for the general structure of the site to the users. 

## Implementation

There is already a `MainMenu` class in **UI -> Modules**. You can add menu items to this class following the instructions from [this page](https://www.msharp.co.uk/#/how-to/menus/creatingMenu).

Once this module class created, it can be added to either individual pages or the header.

### Adding to individual pages
  The main menu module can be added to the root page of any page that showing the main menu is desired.

```csharp
public class ClientPage : RootPage
{
    public ClientPage()
    {
        Add<Modules.MainMenu>();

        OnStart(x => x.Go<Client.ClientsPage>().RunServerSide());
    }
}
```
Then the menu can be `Set()` on the page mentioned on the `OnStart` method. `Set` method is used for showing where to place the menu.

```csharp
public ClientsPage()
{
    Set(PageSettings.LeftMenu, "MainMenu");

    OnStart(x => x.Go<Inventory.CostumesPage>().RunServerSide());
}
```

`PageSettings` include `TopMenu`, `LeftMenu` and `SubMenu` which provide simple styling as default.

### Adding to the header
If you find that adding the menu module in each page is repetitive and cumbersome, as an alternative, you can add the main menu module only to the header:

```csharp
public class Header : GenericModule
{
    public Header()
    {
        IsInUse().IsViewComponent().WrapInForm(false);

        var burger = Link("Burger")
            .NoText()
            .CssClass("navbar-toggler collapsed")
            .Icon(FA.Bars);
            
        Markup($@"
        <nav class=""navbar navbar-expand-md"">
                {burger.Ref}
                <div class=""collapse navbar-collapse"">
                    @(await Component.InvokeAsync<MainMenu>())
                </div>
        </nav>");

        Reference<MainMenu>();
    }
}
```
The `Header` is a placeholder in the `AdminDefault.cshtml` that is used in master page definition in `Project` class inside the #Model project.

```csharp
public Project()
{
    //...
    Layout("Admin default").AjaxRedirect().Default().VirtualPath("~/Views/Layouts/AdminDefault.cshtml");
}
```
The placeholder for **Header** should be in the template cshtml file. This file can be found in the **Website** project in **Views/Layouts/[TEMPLATE].cshtml** path.
```html
<!-- AdminDefault.cshtml -->
<main>
    <header> @await Component.InvokeAsync(typeof(Header)) </header>
    <!--... -->
</main>
```