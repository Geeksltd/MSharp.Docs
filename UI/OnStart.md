# OnStart()

In this lesson we will discuss the `OnStart()` method in M#, which is used to implement page start up code. This is used to implement required actions on page level e.g. redirecting, custom code, roles etc.

Below is code of `DispatchPage` page that used `OnStart()` method:

```csharp
using MSharp;

namespace Login
{
    public class DispatchPage : SubPage<LoginPage>
    {
        public DispatchPage()
        {
            OnStart(x =>
            {
                x.If(AppRole.Admin).Go<AdminPage>().RunServerSide();
                x.GentleMessage("TODO: Add redirect logic here and then delete this activity!");
            });
        }
    }
}
```

M# will generate this:

```csharp
namespace Controllers
{
    [ViewData("Title", "Login > Dispatch")]
    [EscapeGCop("Auto generated code.")]
    public partial class LoginDispatchController : BaseController
    {
        [Route("login/dispatch")]
        public async Task<ActionResult> Index()
        {
            if (User.IsInRole("Admin"))
            {
                return Redirect(Url.Index("Admin"));
            }
            
            Notify("TODO: Add redirect logic here and then delete this activity!", obstruct: false);
            
            return new EmptyResult();
        }
    }
}
```

You can use this method to perform desired actions on page controller e.g. displaying a message, redirecting to other pages based on criteria or any custom code to perform at runtime.