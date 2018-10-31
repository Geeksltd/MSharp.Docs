# Form specific validation

## Problem

Sometimes there might be validation logic which is only meaningful in a specific form and not for the entity in all situations.
M# should and does allow you to write form specific validation code to handle these cases.

When you have some logic which is always needed in the entity, you usually use the `Logic` folder of the `Domain` project and partial classes.
When you need to write some logic which is only valid for a specific form, you can do it in a form specific way.
In this topic we describe how to do so.

## Implementation

`OnBeforeSave()` event of the form module can be used for writing validation code which gets executed before the form gets saved in the database.
We can write custom code for the event like this `OnBeforeSave("some name").Code("//custom code");`.
Since we are writing the code as a string, if it is complicated, we can put the method in a partial clas but still call it from here.

#### Example

Let's say we have a form for entering product details.
There is some very specific logic when entering product data.
We had a special product previously called main which we renamed to CompanySpecial and we want to make employee job easier to change the name of the product whenever they enter this.
Later on we might replace all names including the word main with CompanySpecial but for now let's just rename the product which its name is main.
The form will look like this

```csharp
using MSharp;

namespace Modules
{
    public class ProductForm : FormModule<Domain.Product>
    {
        public ProductForm()
        {
            HeaderText("hey").ValidationStyle(WarningStyle.SummaryBlock);
            Field(x => x.ProductName);
            Field(x => x.Photo);
            OnBeforeSave("Before saving").Code("if(item.ProductName == \"main\") item.ProductName = \"CompanySpecial\";");
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

As you can see we define a `OnBeforeSave()` event with a custom code which checks to see if the name is *main* or not, if yes then it will be changed to *CompanySpecial*.