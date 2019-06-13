# Search field on property

## Problem

When creating a list of items, you will want the user to be able to easily navigate to the rows they need using the properties of each row as search criteria.

## Implementation

In M# we have the `Search()` method where we can pass a list property.

```csharp
Search(x => x.Name);
```

This will then create as default, a search field where a user can type in text and search to see if this text exists in the `Name` data.  This is used in conjunction with the `SearchButton()` method that creates the button you use to return the view of this search.

### Example

Below is an example of the list implementation.

```csharp
    Search(x => x.NameOfContact)
        .Label("Contact")

    SearchButton("Search")
        .OnClick(x => x.ReturnView());

    Column(x => x.NameOfContact);
    Column(x => x.Email);
    Column(x => x.Phone);
    Column(x => x.IsArchived);
```

This will allow the user to search the list of contacts based on the name of contacts.

Below we have the same list but we are now searching the `IsArchived` property. 

```csharp
    Search(x => x.IsArchived)
    .Control(ControlType.HorizontalRadioButtons)
        .Label("Contact")

    SearchButton("Search")
        .OnClick(x => x.ReturnView());

    Column(x => x.NameOfContact);
    Column(x => x.Email);
    Column(x => x.Phone);
    Column(x => x.IsArchived);
```

 Since this property is a `bool` and can only have a maximum of 3 options, we can use the `ControlType` of a horizontal radio button on the UI.

 There are several other `ControlType` options that you can use dependant upon how you wish the control to look for the user such as:

* `AutoComplete` - Good for data that is manageable in size and not too inconvenient to display.

* `DatePicker`, `DateAndTimePicker` - Good for `DateTime` properties.

* `CollapsibleCheckBoxList` - Good for when you want to view multiple data from a property in a single search.

View intellisense for all options on `ControlType`.
