# Index Column

In case you need to have a row counter on any List Module’s generated Html table you can use the IndexColumn method of the fluent API. Bare in mind that no matter where you put the IndexColumn it will always appear as the first column in the generated Html.

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

            IndexColumn(); // generates row counter column
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
