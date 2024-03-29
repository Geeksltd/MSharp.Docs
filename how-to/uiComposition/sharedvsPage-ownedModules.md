# Module: Shared vs page-owned

## Problem

You want to know the difference between shared and page-owned modules and their lifecycle and implications.

For example, for a new Customer form, you may need contact details, billing details, delivery details and preferences. We can have a page for each one of these items and a shared page for basic contact info that is shared among them.

## Difference
Most Modules are used only on one page. In these cases, the page is the owner of the module or the module is page-owned. If the owner has only one module, then the generated code for the page and its modules is merged into a single controller and a view.
  
Modules that are used in more than a page are shared modules. Shared modules are not merged in the page and instead, a separate controller and view are created for them. Depending on whether you want that module to be included in the request lifecycle or binding, you can make a shared module view component or not. In other words, a shared component is not necessarily a view component. These are compared in the following table:

| Specification   |     view componenet     | not view componenet |
| -------|:-------------:|:------------:|
| M# code for the module   | has `IsViewComponent` method | Without `IsViewComponent` method     |
| ASP.Net concept used   | [view components](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/view-components?view=aspnetcore-5.0) | [partial views](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/partial?view=aspnetcore-5.0)|
| Invoked as | `@await Component.InvokeAsync(typeof(ViewName))` | `await Html.PartialAsync(ViewName, ViewBag.ViewName as ViewModel.ViewName)`     |
| Generated files paths in the Website project  | Views/Modules/Componenets Controllers/Modules/Componenets | Views/Modules Controllers/Modules      |
| Page lifecycle  | Don't take part in the containing page lifecycle | Have the same lifecycle as their containing pages for requests and bindings     |
| Typical usage  | More suited to layout sections in the master pages like header and menus | Main content parts like entity lists or forms      |

## Shared module parameters
You can create a shared module that is used in multiple places with different configurations being set on the owner page. In these cases, the shared module has parameters that are set in the owner instead of the query string.
## Example
Suppose that we have a shared module with a `Mode` property. Depending on this property, view elements like header are changed inside the shared module.
```csharp
public class SharedView : GenericModule
{
    public SharedView()
    {
        HeaderText("SharedView @info.Mode");
        ViewModelProperty<string>("Mode");
    }
}
```
We can use this module in the enter page with the `Mode` being set to `Enter`.
```csharp
public class EnterPage : SubPage<Page>
{
    public EnterPage()
    {
        //...
        Add<Modules.SharedView>().OnBinding("info.Mode = \"Enter\";");
    }
}
```
On the other hand, we can use this module in the view page with the `Mode` being set to `View`.
```csharp
public class ViewPage : SubPage<Page>
{
    public ViewPage()
    {
        //...
        Add<Modules.SharedView>().OnBinding("info.Mode = \"View\";");
    }
}
```
## Binding conflict in pages with multiple modules
When you use multiple modules on a page, you may encounter a binding conflict. This can be avoided with using `Prefix` method.
## Example
Suppose that we have two list modules in a page and both modules are using searching and paging. 
```csharp
public class SummaryPage : RootPage
{
    public SummaryPage()
    {
        //...
        Add<Modules.ProjectsList>();
        Add<Modules.ClientsList>();
    }
}
```
If we run this page without any other change, you will see that searching is applied to both lists since the query string is bound to both of them. If you want to separate them from each other and limit the scope of the binding, you need to use `Prefix` in module classes with different values.
```csharp
public class ProjectsList : ListModule<Domain.Project>
{
    public ProjectsList()
    {
        Prefix("pl");
        //...
    }
}
```
```csharp
public class ClientsList : ListModule<Domain.Client>
{
    public ClientsList()
    {
        Prefix("cl");
        //...
    }
}
```
This change is reflected in the generated code as changing the ViewModel class to use binding prefix and `[FromQuery]` attribute. More information can be found [here](https://docs.microsoft.com/en-us/aspnet/core/mvc/models/model-binding?view=aspnetcore-5.0#complex-types).
```csharp
public partial class ContactsList : IViewModel
{
    public ContactsList()
    {
        Paging = new ListPagination(this, 10) { Prefix = "cl" , UseAjaxGet = true };
        Sort = new ListSortExpression(this) { Prefix = "cl" };
    }
        
    [FromQuery(Name = "cl.s")]
    public ListSortExpression Sort { get; set; }
        
    [FromQuery(Name = "cl.p")]
    public ListPagination Paging { get; set; }
        
    // Search filters
    [FromQuery(Name = "cl.FullSearch")]
    public string FullSearch { get; set; }

    //...
}
```