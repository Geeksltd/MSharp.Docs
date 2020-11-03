# Master Detail Forms

## Problem

If entity A has a one to many relationship with entity B, you may want to edit and add B entities to Entity A from an Entity A form.

For example, Companies can have multiple Properties. Each Property has a Street Address, Postcode and a Phone Number. You want to be able to edit these properties from a single Company Form instead of having to enter them into individual Property forms.

## Implementation

You can achieve this goal by using Master Detail Forms.

Master Detail Forms have a Master section with fields on entity A and then a sub form, the Detail section, for entity B of which there can be many.
In this case the Company fields are the Master part of the form and the Property fields are the Detail part of the form

```csharp
public CompanyForm()
{
    HeaderText("Company Details");

    Field(x => x.Name);
    Field(x => x.Sector);
    Field(x => x.Contact);

    MasterDetail(x => x.Properties, s =>
    {
        s.HeaderText("Serviced Properties");
        s.Field(x => x.StreetAddress);
        s.Field(x => x.Postcode);
        s.Field(x => x.PhoneNumber);

        s.Button("Add Property").OnClick(x => x.AddMasterDetailRow());
    }).MinCardinality(1);

    Button("Cancel").OnClick(x => x.CloseModal());

    Button("Save").IsDefault().Icon(FA.Check)
        .OnClick(x =>
        {
            x.SaveInDatabase();
            x.GentleMessage("Saved successfully.");
            x.CloseModal(Refresh.Ajax);
        });
}
```

Using `MasterDetail()`, the first parameter defines which property the detail form is for, the second allows you to configure the detail form to your specification.
You can add Fields, Buttons, Headers etc, just as you would in a normal form.

Of particular note is the Button “Add Property”, `OnClick()` it adds a new row which allows the User to add more instances of Property, this is especially important if you do not know how many instances the user will require.

Here the `MinCardinality()` has been set to 1, this means at least 1 Property must be added. There are also methods for `InitialCardinality()` and `MaxCardinality()`.
