# Search Field on Property

## Problem

There are a lot of items in a list and you need to be able to search for specific entries based on their properties.

## Implementation

Using Search(x=> x.Property) allows you to search by any property of the entity.

```csharp

public ContactsList()
    {
        HeaderText("Contacts");

        Search(x => x.Category)
            .AsRadioButtons(Arrange.Horizontal)
	    .DataSource("#ALL#")
            .Label("Classification")
            .ReloadOnChange();
        Search(x => x.Name)
            .NoLabel()
            .WatermarkText("Enter Name");
            
        SearchButton("Search").OnClick(x=>x.Reload());

        Column(x => x.Category);
        Column(x => x.Name);
	}

```

Useful Methods Include:

- AsCheckbox(), AsRadioButtons(), ... - set the input type

- DataSource("#ALL#") - Displays all options instead of only those with results

- Label() – change the label text, default is the property name

- WatermarkText() – Add a watermark to text fields

- ReloadOnChange() – Have the page reload automatically on entry without having to press a Search button.

For selectable choices, by default, M# will add a pseudo first option in the list, reading "-Select-". In cases where the field is `mandatory` and you always have a `default value`, then that first option will become meaningless. In such case, you can remove it by setting `Field(x => x.Something).NoWatermarkText()`.

You can add a Search button if it is required.
