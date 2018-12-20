# Adding Checkbox

## Problem

By default, when defining form fields, M# chooses control types for you but if you want to define a checkbox specifically, you can tell M# to do so, regardless of the data-type of the property.

## Implementation

The `Control()` method can be used on fields to choose their control type.
If you supply `ControlType.Checkbox` then the control will be a checkbox.

#### Example

Let's define a product form which contains a checkbox for used products.

```csharp
using MSharp;

namespace Modules
{
    public class ProductForm : FormModule<Domain.Product>
    {
        public ProductForm()
        {
            Field(x => x.ProductName).Control(ControlType.Textbox);
            Field(x => x.IsUsed).Control(ControlType.CheckBox);
            Button("Save").IsDefault().Icon(FA.Check).OnClick(x =>
            {
                x.SaveInDatabase();
                x.GentleMessage("Saved");
                x.ReturnToPreviousPage();
            });
        }
    }
}
```

![checkbox](images/checkbox.PNG)

As you can see we set the control type of the bool field as Checkbox but we could do the same with other types which their default is not a bool as well.
