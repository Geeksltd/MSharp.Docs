# Adding a Button

## Problem

When working with M#’s modules, especially form modules, users need to perform certain workflows like Save the form or Cancel submission. In order to enable users to perform such actions you need to add buttons to your modules.

## Implementation

To add a button to a M# module, use the Button method. Pass the desired name of the button to its first argument like below and chain the method with OnClick method to provide the workflow like below:

```csharp

class SlideFrm : FormModule<Domain.Slide>
    {
        public SlideFrm()
        {
            HeaderText("Slide details");
            
            Field(x => x.Title);
            Field(x => x.Description);
            Field(x => x.DisplayOrder);
            Field(x => x.Image);        

            Button("Cancel")
                .OnClick(x => x.Go<Admin.SlidesPage>());
            
            Button("Save")
                .IsDefault() 
                .Icon(FA.Check)
                .OnClick(x =>
                {
                    x.SaveInDatabase();
                    x.GentleMessage("Saved successfully.");
                    x.Go<Admin.SlidesPage>();
                });
        }
    }

```

Here is the list of most used methods you can chain with Button method:

* Icon(FA icon) or Icon(string value): to add an icon to the button, M# natively supports Font Awesome.
* ImageUrl(string value): Set an Image URL for the button. Usually used in conjunction with NoText().
* IsDefault(bool? value = true): in case of having multiple buttons use this method on one of them to visually separate it from the rest of buttons. 
* Name(string value): to change the name attribute of the generated Html of the button
* Tooltip(string value): for adding the text which will be shown to the user on mouse hover event
* ConfirmQuestion(string value): On clicking the button, Pops up a confirmation dialogue with the provided message
