# Merged Forms

## Problem

If Entity A has a one to one relationship with Entity B, you might want to be able to define the properties for Entity B in an Entity A form.

For example, each Contact has an Address property. Each Address has a Street Address, City and Post Code. You want to be able to define the Address properties for the associated Contact, within a Contact form.

## Implementation

You can achieve this by using Merged Forms.

This provides a sub form, the Merged Form, for Entity B, as part of the main form used for Entity A. In this case, the Contact form contains the Contact properties, whilst also providing the Address properties as part of the Merged Form.

```csharp
public ContactForm()
{
    HeaderText("Contact Details");

    Field(x => x.Name);
    Field(x => x.Email);

    MergedForm(x => x.Address, y =>
    {
        y.Field(x => x.StreetAddress);
        y.Field(x => x.City);
        y.Field(x => x.PostCode);
    });

    Button("Cancel")
        .OnClick(x => x.ReturnToPreviousPage());

    Button("Save").IsDefault().Icon(FA.Check)
        .OnClick(x =>
        {
            x.SaveInDatabase();
            x.GentleMessage("Saved successfully.");
            x.ReturnToPreviousPage();
        });
}
```

Using MergedForm(), the first parameter defines the property that the merged form is being used for, whilst the second parameter is used for defining the fields in the merged form.
