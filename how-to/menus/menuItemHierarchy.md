# Menu item hierarchy

## Problem

The client wants to have nested items in the menu structure in the form of parent-child or item-subitem form to categorize items and showing them all in one menu at the same time.

## Implementation

You can create a hierarchy in menu items using two methods `SubItem` and `Parent`.

```csharp
public class SettingsMenu : MenuModule
{
    public SettingsMenu()
    {
        //...
        SubItemBehaviour(MenuSubItemBehaviour.ExpandCollapse);

         var adminMenu = Item("Admin")
            .CssClass("has-submenu");
         adminMenu.SubItem("Users")
            .OnClick(x => x.Go<UsersPage>());
         
        var settings = Item("Settings");
        Item("General Settings").Parent(settings)
             .OnClick(x => x.Go<GeneralPage>());

    }
}
```
`SubItemBehaviour` method is used to set how showing subitems in the menu handled. It takes an argument of enum type `MenuSubItemBehaviour` which take the following values:

- `ClickDropDown`:  Subitems are shown when the parent item is clicked.

- `HoverDropDown`: Subitems are shown when the mouse is pointed to the parent item.

- `ExpandCollapse`: Clicking the parent item causes the subitems to expand and being shown. Another click to the same item or other parent items collapses the hierarchy.

- `Accordion`: subitems are shown in a vertically stacked list that can be clicked to reveal or hide like an accordion.


Note:

> The solution presented here for hierarchical menu items applies only to static menu items. If you have dynamic menu items with an unknown level of nesting, you should use another solution like rendering the menu using Treeview. We have plans to support these scenarios in M# in the future.