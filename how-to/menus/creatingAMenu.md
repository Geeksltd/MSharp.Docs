# Creating a menu

## Problem

When creating an application, it needs to be easy for your user to be able to navigate to different areas of the application intuitively.  Menus are a great way to allow your user to do this.

## Implementation

When creating an M# project, a folder called "-Menus" would have been created as one of the default folders.  In this folder there will already be an `AdminSettingsMenu.cs` and `MainMenu.cs` file.  What is key to creating a menu is that the class should inherit from the `MenuModule` class in order to work as a menu in the project.  

Each menu item you wish to create can be created using `Item()` and you can use the `OnClick()` method to define where the user is navigated to when clicking on this menu item using `Go<>`.

```csharp
Item("General settings")
                .OnClick(x => x.Go<Admin.Settings.GeneralPage>());
```

### Examples

This is the default content of the `AdminSettingsMenu.cs` file

```csharp
using MSharp;
using Domain;

namespace Modules
{
    public class AdminSettingsMenu : MenuModule
    {
        public AdminSettingsMenu()
        {
            IsViewComponent().RootCssClass("navbar navbar-light").UlCssClass("nav flex-column w-100");

            Item("General settings")
                .OnClick(x => x.Go<Admin.Settings.GeneralPage>());

            Item("Administrators")
                .OnClick(x => x.Go<Admin.Settings.AdministratorsPage>());

            Item("Content blocks")
                .OnClick(x => x.Go<Admin.Settings.ContentBlocksPage>());
        }
    }
}
```
