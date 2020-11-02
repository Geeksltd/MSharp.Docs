# Trigering/skipping validation

When working on M# form modules sometimes we need to allow the user to complete the form partially or without accurate input, for example when developing the form and we just need some dummy data for testing purposes. In order to instruct M# to lift any validations’ defined on the entity we should chain the Button method with the `CauseValidation` and enter false for its first argument.



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
                .CausesValidation(false)
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