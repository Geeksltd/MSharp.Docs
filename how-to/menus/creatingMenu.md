# Creating a Menu

## Problem

Although MSharp has a Main Menu as standard, your application is too complex and requires more menus in order to maintain usability. 

## Implementation

When arranged in a methodical and hierarchical structure, menus enable easy navigation around the site while also providing a visual representation of the structure of the site to the user.

Fortunately MSharp makes Menus easy.

Menus can be added to UI -> Modules. Right clicking on the menu folder will allow you to add a new M# menu item, which provides a handy template.

```csharp

using MSharp;

namespace Modules
{
    class AdminInventoryMenu : MenuModule
    {
        public AdminInventoryMenu()
        {
            AjaxRedirect();
            IsViewComponent();
            UlCssClass("nav navbar-nav dropped-submenu");
            RootCssClass("sidebar-menu");

            //Can be implemented this way:
            Item("Costumes")
                .OnClick(x => x.Go<Inventory.CostumesPage>());

            //or this way:
            Item<Inventory.GadgetsPage>("Gadgets");

            Item("Weapons")
                .OnClick(x => x.Go<Inventory.WeaponsPage>())
                .VisibleIf(AppRole.Admin)
                .Icon(FA.Hammer);
        }
    }
} 

```

There are many methods which can be applied to the menu, here extra CSS classes have been added for styling.

Useful methods for items include:

- `OnClick()`: Determines the destination of the link

- `VisibleIf()`: Especially useful with AppRole allowing for a different user experience depending on the role of the User.

- `Icon(FA icon)` or `Icon(string value)`: to add an icon to the button, M# natively supports Font Awesome.

Once created, the Menu can be `Set()` on any pages you want, the use of root pages is very useful in this endeavour. 

```csharp

        public InventoryPage()
        {
            Set(PageSettings.LeftMenu, "AdminInventoryMenu");

            OnStart(x => x.Go<Inventory.CostumesPage>().RunServerSide());
        }

```

`PageSettings` include `TopMenu`, `LeftMenu` and `SubMenu` which provide simple styling as standard but you can add your own if you fancy a challenge.
