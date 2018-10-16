# Global Search

In some scenarios, you may need to search through arbitrary pages and let users easily navigate among them. For this purpose there is a file named `GlobalSearchSource.cs` that is located at this path `Website > app_Start > Extensions`. Here at this file, you can add your custom resources as shown below:

```csharp
public class GlobalSearchSource : SearchSource
{
    public override async Task Process(ClaimsPrincipal user)
    {
        Add(new SearchResult()
        {
            Title = "Administrators",
            Description = "administrators list",
            Url = "/admin/settings/administrators",
            IconUrl = ""
        });

        Add(new SearchResult()
        {
            Title = "Contents",
            Description = "content blocks list",
            Url = "/admin/settings/content-blocks",
            IconUrl = ""
        });

        //TODO: Please add custom search data here
    }
}
```

As you can see, we have added two pages **Administrators** and **Contents** and if users search these names they can easily navigate to the destination page.