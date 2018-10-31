# Adding TextBox

## Problem

When you are creating forms, M# chooses default controls for different data-types but sometimes you want to change the control or limit the possible values.
Let's take a look at how to define a textbox.

## Implementation

When you define a form field using the `Field()` method, M# automatically chooses a control type based on the data-type of the field. 
For string and numeric data-types M# chooses the textbox control.

However if you specifically want to define a textbox as the control for a field, you can do so by calling the `Control()` fluent method on the field.
The `Control()` method takes an enum of type `ControlType` as its parameter which contains all possible control types which you can define without custom raw HTML code.

#### Example

Let's define a simplistic form for our product which asks for the product's name.
The product entity is a very simple one which doesn't need definition here.

```csharp
using MSharp;

namespace Modules
{
    public class ProductForm : FormModule<Domain.Product>
    {
        public ProductForm()
        {
            Field(x => x.ProductName).Control(ControlType.Textbox);
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

![textbox](images/textbox.PNG)

The `ProductName` property is a string and would have a textbox as the control type anyways but here is how to define it explicitly.
sometimes you might want to define the control type of other data-types as textbox which explicit definition will be useful for.

## Remarks

If you want to make the textbox multi-line, call the `Lines()` method on the property definition when defining the entity.