# Visibility

## Problem

Not all information on a page is relevant to all users at all times. To avoid cluttering the UI with unnecessary, repeated or unauthorised content you can make elements visible only under  specific circumstances.

This allows for more dynamic content and less repetition of code.

## Implementation

Visibility can be changed on a variety of elements, including columns, buttons, menu items and whole modules.

`VisibleIf()` can be invoked by writing the desired code in a string, this code is then generated in the Cshtml file.

Often you want to limit visibility based on the Users role, in this case you can invoke `VisibleIf()` using `AppRole`. 

## Examples

### List Columns

If a Contacts List is filtered by query string “category” the Category column should not be displayed.

```csharp
    Column(x => x.Category).VisibleIf("info.Category == null");
```

To only effect the visibility of certain cells in a column, depending on item, use `CellVisibleIf()`.

### Using AppRole

A menu item should only be seen by Users with an admin role.

```csharp
    Item("Admin Only Page")
        .VisibleIf(AppRole.Admin)
        .OnClick(x => x.Go<Admin.AdminPage>()
```

### Button Columns

Only Admin Users can view the button column, a button should only be visible if the list item has any Contacts to view

```csharp
    ButtonColumn("View")
        .ColumnVisibleIf(AppRole.Admin)
        .VisibleIf("await item.Contacts.Any()")
        .HeaderText("Contacts")
        .GridColumnCssClass("actions")
        .Icon(FA.AddressBook)
        .OnClick(x => x.Go<ContactsPage>().Send("item", "item.ID"));
```

On a button column `VisibleIf()` affects the visibility of the individual buttons, so to hide the column use `ColumnVisibleIf()`. 