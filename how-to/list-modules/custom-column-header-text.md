# Custom Column Header Text

You can change the column’s header text by using the HeaderTemplate method of the fluent API. Not only you can specify the name of the column, you can also change the markup inside the th element.

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

            Column(x => x.Title).HeaderTemplate("<strong>Title</strong>");
            Column(x => x.Description);
            Column(x => x.LinkUrl).HeaderTemplate("Url");
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
