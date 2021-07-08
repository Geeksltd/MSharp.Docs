# Auto page redirection

## Problem

You want a page to be redirected automatically to another page within the same website and resolve an existing URL for the page to a different one.

## Usage patterns

You may want to redirect to another page for one of the following reasons:

- **Access right**: You want only a subset of users with necessary privileges visit the page. If the user has not logged in or don't have the desired privilege then being redirected to the login or error page.
- **Security**: You trust a third party such as Google, Facebook or Microsoft, for user authentication using security mechanisms such as OAuth and OpenID for social media login. In this way, the login page on your website will be redirected to the 3rd party provider.
- **Query parameters**: UI module is defined in a way that is using query string parameters for showing, resolving or filtering data. If query parameters aren't provided, the page is redirected.
- **Menu highlighting**: You have a navigation menu that when items are clicked, highlight the menu item to show the current navigated page. When the page is invoked from a link other than the menu, we may redirect the page to be invoked from the menu the get the menu highlighting right.

## Implementation
Redirection logic can be placed in `OnStart` method to be executed automatically when the page is invoked. Olive framework has `Redirect` method that can be used to redirect to the desired URL.

### Example
Typical usage of redirection can be used in the `LoginPage`.

```csharp
public class LoginPage : RootPage
{
    public LoginPage()
    {
        //...
        OnStart(x =>
        {
            x.If("Request.IsAjaxPost()")
                .CSharp("return Redirect(Url.CurrentUri().OriginalString);");
            x.If("User.Identity.IsAuthenticated")
                .Go<Login.DispatchPage>().RunServerSide();
            x.If("Url.ReturnUrl().IsEmpty()")
                .Go("/login").RunServerSide()
                .Send("ReturnUrl", ValueContext.Static, "/login");
        });
    }
}
```
In this code multiple conditions are checked using the `If` method based on the request type, authentication and query string and for each satisfied condition redirection to a different page is specified by using the target page explicitly with `Go` method or with running a C# expression containing the `Redirect` method.
