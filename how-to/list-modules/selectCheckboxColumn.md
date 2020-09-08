# Select Checkbox Column

## Problem

The Client wants to be able to perform an action on multiple list items.

For example, the Client wants to be able to mark multiple contracts as authorised when they click the Authorise button.

## Implementation

When `SelectCheckbox()` is true, MSharp generates a column of checkboxes allowing the user to select items in the list. By default the checkbox column will be the first column, however you can customise this with `SelectCheckboxColumnIndex()`.

```csharp
    public ContractList()
    {
        HeaderText("Contracts");
            
        SelectCheckbox(true);
        SelectCheckboxColumnIndex(3);
            
        Column(x => x.ID);
        Column(x => x.IsAuthorised);
        Column(x => x.StartDate);

        Button("Authorise")
            .OnClick(x => 
            {
                x.CSharp("await Contract.Authorise(info.SelectedItems);");
                x.Reload();
            });
    }
```

You can reference the selected items using `info.SelectedItems`.
In this example, there is an authorise button that calls a method in the Domain that will set IsAuthorised to true for all the Selected Items.

In the Domain:

```csharp
    public static async Task Authorise(Task<IEnumerable<Contract>> contracts)
    {
        await Database.Update<Contract>(await contracts, async x => x.IsAuthorised = true);
    }
```