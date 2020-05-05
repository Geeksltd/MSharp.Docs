# Hiding/Showing Buttons

In situations in which we need to show a button or link only if some criterias are met, we can chain the button method of the fluent api with VisibleIf method which requires the condition validator.

M# has the most common criterias built in which you can invoke by using the CommonCriterion enum. The example below is taken from the default M# project template, specifically the Header module located under #UI > Modules > -Custom > Header.cs

```csharp
using MSharp;
using Domain;

namespace Modules
{
    public class Header : GenericModule
    {
        public Header()
        {
            IsInUse().IsViewComponent().WrapInForm(false);
            WrapInForm();
            Using("Olive.Security");
            RootCssClass("header-wrapper");
            var logo = Image("Logo").CssClass("logo").ImageUrl("~/img/Logo.png")
                  .OnClick(x => x.Go("~/"));

            var burger = Link("Burger")
                .NoText()
                .Icon("fas")
                 .CssClass("menu-toggler burger-icon")

                .ExtraTagAttributes("type=\"button\"");

            var login = Link("Login").Icon(FA.UnlockAlt)
                        .VisibleIf(AppRole.Anonymous)
                        .OnClick(x => x.Go<LoginPage>());

            var logout = Link("Logout")
                         .CssClass("align-bottom logout")
                         .ValidateAntiForgeryToken(false)
                         // The logout button is only visible to loggedin users
                         .VisibleIf(CommonCriterion.IsUserLoggedIn)
                         .OnClick(x =>
                         {
                             x.CSharp("await OAuth.Instance.LogOff();");
                             x.Go<LoginPage>();
                         });
            Markup($@"
            <nav class=""navbar"">
              <div class=""header-left-actions-wrapper"">
                      {burger.Ref}
                      {logo.Ref}
              </div>
              <div class=""header-account-wrapper"">
                    {logout.Ref}
                  </div>
            </nav>");
        }
    }
}
```