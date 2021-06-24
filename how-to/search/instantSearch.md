# Instant Search

## Problem

The client wants to perform a search on the client-side and see the results instantly without pressing any button.

## Implementation

M# built-in Search supports client-side searching and filtering, as shown below:

```csharp
public ContactsList()
{
   //...
   Search(GeneralSearch.ClientSideFilter)
       .WatermarkText("Search...")
       .NoLabel();
}
```

In this code:
- `Search(GeneralSearch.ClientSideFilter)` – Make Search filters that do not depend on a property and works without pressing a button on the client-side.
- `WatermarkText("Search...")` – Places the specified text as a watermark inside the search box. It will be removed as soon as the user starts typing. 
- `NoLabel()` – No label is used for the search box because the purpose is specified with the watermark text. 

### Generated code
The generated code for the above code creates the following section in the markup:

```html
<!-- ContactContacts.cshtml-->
<div class="search">
   <div class="form-group row">
      <div class="group-control">
         <input type="text" asp-for="InstantSearch" class="form-control" placeholder="Search..." />
      </div>
   </div>
</div>
```

and the controller class will be changed in the `GetSource()` method by using the ViewModel property `InstantSearch`:

```csharp
public partial class ContactContactsController : BaseController
{
    //...

   [NonAction]
   async Task<IEnumerable<Contact>> GetSource(vm.ContactsList info, bool all = false)
   {
        var query = Database.Of<Contact>();           
        var result = await query.GetList();     
        if (info.InstantSearch.HasValue())
        {
            var keywords = info.InstantSearch.Split(' ').Trim().ToArray();
            result = result.Where(item => item.ToString("F").ContainsAll(keywords, caseSensitive: false));
        }
        //...
    }
}

public partial class ContactsList : IViewModel
{
    //...

    // Search filters
    public string InstantSearch { get; set; }
}
```
