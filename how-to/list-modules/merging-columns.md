# Merging Columns

In case you need to merge multiple columns based on the data inside each column you might end up in following situations:

1. **You have multiple link or button columns which you wish to merge in a single column:** in this situation you can use HeaderText method of the fluent API. ButtonColumns or LinkColumns with the same header text will be merged into a single column.

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

            ButtonColumn("Edit")
                .HeaderText("Actions")
                .Icon(FA.Edit)
                .OnClick(x => x.Go<Admin.Slides.AddOrUpdatePage>().Send("item", "item.ID"));

            ButtonColumn("Delete")
                .HeaderText("Actions")
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

2. **You have multiple properties in your model which you wish to merge into a single column but also like to format the end result:** you’re better off using custom display expression. For more information please visit [Custom display expression/format](how-to/list-modules/custom-display-expression-format.md)

3. **You have multiple properties in your model which you like to merge without any formatting:** use the _NeedsMerging_ method of the fluent API which merges the current column with the previous one.

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
            Column(x => x.LinkText);
            Column(x => x.LinkUrl).NeedsMerging(); // Merges LinkUrl with previous coloumn (LinkText)
            Column(x => x.DisplayOrder);
            Column(x => x.Image);

            ButtonColumn("Edit")
                .HeaderText("Actions")
                .Icon(FA.Edit)
                .OnClick(x => x.Go<Admin.Slides.AddOrUpdatePage>().Send("item", "item.ID"));

            ButtonColumn("Delete")
                .HeaderText("Actions")
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

> Note: The generated merged td element will just concat the data for each merge property, no formatting will be applied on the end result.
