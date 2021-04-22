# Page Start-Up Logic

## Problem

You want to carry out specific logic, whenever a user navigates to the page.

A common example is when a user logs in and the application needs to redirect the user to the correct page, based on their given role.

## Implementation

With MSharp, you can achieve this by using `OnStart()` on the page itself.

```csharp
public class DispatchPage : SubPage<LoginPage>
{
    public DispatchPage()
    {
        OnStart(x =>
        {
            x.If(AppRole.Admin).Go<AdminPage>().RunServerSide();
            x.ElseIf(AppRole.Manager).Go<ManagerPage>().RunServerSide();

            /*
            * Additional code for handling redirecting the user based on their role
            */
        });
    }
}
```
