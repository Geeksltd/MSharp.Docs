# Custom page URL

## Problem

Sometimes, when a page is deeply nested, the URL for that page can be quite long.  There will be times when you want to shorten this for readability.

## Implementation

We can define the URL we wish to use using the `Route()` method.  By passing our new desired URL path, we can override the default URL for this page.

### Example

```csharp
namespace WebMain
{
    public class AboutUsPage : SubPage<WebMainPage>
    {
        public AboutUsPage()
        {
            Route(@"about-us");
            Layout(Layouts.Webpage);

            Add<Modules.WebpageAboutUsList>();
        }
    }
}
```

This example shows a simple "About Us" page.  Given the nature of the page, we don't want the URL to be too convoluted. Overriding the URL makes it more simple to navigate to using the URL string.
