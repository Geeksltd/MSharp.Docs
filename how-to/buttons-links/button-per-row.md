# Button Per Row

When working on *list modules* by default data is represented via an Html table, in some scenarios we need to add buttons on each row to perform certain workflows for example edit or delete the record. To do so, you can use M#’s ButtonColumn method like below:

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
            
            Column(x => x.Title);
            Column(x => x.Description);
            Column(x => x.LinkUrl);
            Column(x => x.LinkText);
            Column(x => x.DisplayOrder);
            Column(x => x.Image);

            ButtonColumn("Edit")
                .HeaderText("Actions")
                .GridColumnCssClass("actions")
                .Icon(FA.Edit)
                .OnClick(x => x.Go <Admin.Slides.AddOrUpdatePage> ().Send("item", "item.ID"));

            ButtonColumn("Delete")
                .HeaderText("Actions") // The column header text, also used for grouping buttons
                .GridColumnCssClass("actions") // M# adds this class to all cells on the column
                .Icon(FA.Remove)
                .ConfirmQuestion("Are you sure you want to delete this slide?")
                .CssClass("btn-danger") // M# adds this class to the button itself
                .OnClick(x => {
                    x.DeleteItem();
                    x.RefreshPage();
                });


            Button("New Slide")
                .Icon(FA.Plus)
                .IsDefault()
                .OnClick(x => x.Go <Admin.Slides.AddOrUpdatePage> ());
        }
    }
}


```

Provide the text of the button with the ButtonColumn method’s first argument. You can add an icon to the button by chaining the ButtonColumn method with Icon method.

You can group buttons on a column by providing the same header text for each button, M# will group buttons with the same header text to a column.
