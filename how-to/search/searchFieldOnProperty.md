# Search Field on Property

## Problem

There are a lot of items in a list and you need to be able to search for specific entries based on their properties.

## Implementation

Using `Search(x=> x.Property)` allows you to search by any property of the entity.

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
            
        SearchButton("Search").OnClick(x => x.Reload());

        Column(x => x.Category);
        Column(x => x.Name);
	}

```

Useful Methods Include:

- `AsCheckbox()`, `AsRadioButtons()`, ... set the input type
- `DataSource("#ALL#")` or simply `ShowAllRecords()` displays all options in the database instead of only those used within the results
- `Label(...)` changes the label text, default is the property name
- `Label("#EMPTY#])` or simply `.NoLabel()` removes the label.
- `WatermarkText(...)` add a placeholder to text fields. For dropdown list and other select controls, it allows you to change `-Select-` to your desired text.
- `ReloadOnChange()` means the page reloads automatically on data entry without having to press a Search button.
- `NoWatermarkText()` removes the 'All' option (in dropdown list and other select controls).

