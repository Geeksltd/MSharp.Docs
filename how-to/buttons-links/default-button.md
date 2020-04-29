# Default Button

When working with multiple buttons or links you can designate only one of which as the default button. The default button or link has visual contrast with the reset and the rendered html element has its default-button attribute set to true.

In order to select a button as the default button just chain the Button method with the IsDefault() method like below:

```csharp

using MSharp;

namespace Modules
{
    class CategoryFrm : FormModule<Domain.Category>
    {
        public CategoryFrm()
        {
            HeaderText("Category details");
            
            Field(x => x.Name);
            
            Button("Cancel").OnClick(x => x.ReturnToPreviousPage());
            
            Button("Save")
            .IsDefault()
            .Icon(FA.Check)
            .OnClick(x =>
            {
                x.SaveInDatabase();
                x.GentleMessage("Saved successfully.");
                x.Go<Admin.CategoriesPage>();
            });
        }
    }
}

```