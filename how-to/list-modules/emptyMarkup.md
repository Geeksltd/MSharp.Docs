# Empty Markup

## Problem

You want a specific message displayed when the list contains no records.

## Implementation

The default message is “There are no _ to display.” However this is not always desired or appropriate. Using EmptyMarkup()  you can set the message using plain text or html.

```csharp
    public EmployeeList()
    {
        HeaderText("Staff")
            .EmptyMarkup("No staff records found");
        /*
        * other code
        */
    }
```

To have no empty markup use `.EmptyMarkup(“[#EMPTY#]”)` or `.NoEmptyMarkup()`

Empty Mark up can also be applied to fields with no value.

```csharp
    Column(x => x.FirstName);
    Column(x => x.LastName);
    Column(x => x.Address).EmptyMarkup("[#BUTTONS(AddAddress)#]");

    Button("Add Address").OnClick(x => x.PopUp<Address.EnterPage>());
```

Here if the record has no value for the address it will instead display a button that will open a pop up for the User to enter a new address
