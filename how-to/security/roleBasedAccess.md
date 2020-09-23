# Role Based Access

## Problem

You want to limit who has access to certain pages of the application.

For example, only Admin Users should be able to access the Settings page but everyone can view the Products page.

## Implementation

This page covers

1. Creating new roles
2. Hiding content based on role
3. Limiting page access to specific roles

### Creating Roles

The Admin user is automatically generated, and access based on Admin role can be applied easily. If you require further roles they can be defined in the Model in Project.cs.

Here, the Employee role has been added.

```csharp
    Role("Local.Request");
    Role("Anonymous");
    Role("Admin").SkipQueryStringSecurity();
    Role("Employee");
```

To give Employee users the Employee role you will need to add a GetRoles() method to Domain > Logic > Employee.cs. This method will override the one found in the User logic.

```csharp
    partial class Employee
    {
        /// <summary>Gets the roles of this user.</summary>
        public override IEnumerable<string> GetRoles() => base.GetRoles().Concat("Employee");
    }
```

### Hiding Unauthorised Content

This includes hiding buttons and menu links from Users who do not have appropriate access. This hinders their access to the page but also provides a better User Experience for everyone as only buttons that the User can use are visible to them.

You can use VisibleIf() to hide buttons, columns, even whole modules depending on role.

```csharp
    public MainMenu()
    {
        /*
        * other code
        */

        Item("Employees")
            .OnClick(x => x.Go<Employee.EmployeesPage>());

        Item("Products")
            .VisibleIf(AppRole.Employee, AppRole.Admin);
            .OnClick(x => x.Go<Employee.ProductsPage>())

        Item("Settings")
            .VisibleIf(AppRole.Admin)
            .OnClick(x => x.Go<Admin.Settings.GeneralPage>());
    }
```

In this example:

- Employees can be seen by anyone
- Products can be seen by Employees and Admins
- Settings can only be seen by Admins.

### Limiting Page Access

Removing all the links to a page doesn’t stop people from navigating to a page using the URL.

To stop this, add Roles to your pages.

Roles can be added to any pages but are most powerful when added to a root page, preventing access to its subpages too.

```csharp
public class AdminPage : RootPage
{
    public AdminPage()
    {
        Roles(AppRole.Admin);

        Add<Modules.MainMenu>();

        OnStart(x => x.Go<Admin.SettingsPage>().RunServerSide());
    }
}
```

Now, only Admin users can access any Admin pages even with the URL.
