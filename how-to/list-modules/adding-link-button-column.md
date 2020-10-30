# Adding link/button column

When we’re working with list modules, usually we need to provide the user with some functionalities for each entity eg. edit, delete etc. To do so, we must use the ButtonColumn method of the fluent API. For more information about Buttons please check the How-to: Buttons/Links section.

```csharp
using MSharp;

namespace Modules
{
    class SlideTbl : ListModule<Domain.Slide>
    {
        public SlideTbl()
        {
            HeaderText("Slides");
            
            Search(GeneralSearch.AllFields).Label("Find:");
            SearchButton("Search").OnClick(x => x.Reload());
            
            Column(x => x.Title);
            Column(x => x.Description);
            Column(x => x.LinkUrl);
            Column(x => x.LinkText);
            Column(x => x.DisplayOrder);
            Column(x => x.Image);

            // Adds a button named Edit under Actions column
            ButtonColumn("Edit")
                // The header text of the column
                .HeaderText("Actions")
                // css class of the column
                .GridColumnCssClass("actions")
                .Icon(FA.Edit)
                .OnClick(x => x.Go<Admin.Slides.AddOrUpdatePage>().Send("item", "item.ID"));

            // Adds a button named Delete and merges this column 
            ButtonColumn("Delete")
                // merges this column with the previous column eg. Actions column
                .NeedsMerging()
                .CssClass("btn-danger")
                .Icon(FA.Remove)
                .OnClick(x => {
                    x.DeleteItem();
                    x.RefreshPage();
                });

            Button("New Slide")
                .Icon(FA.Plus)
                .OnClick(x => x.Go <Admin.Slides.AddOrUpdatePage>());
        }
    }
}
```