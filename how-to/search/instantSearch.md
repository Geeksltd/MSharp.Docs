# Instant Search

## Problem

The client would like to have a list refreshed as soon as a search filter gets updated.

For example, they want to search for all Employees within a specific Department and would like the list to be instantly updated, based on their selection.

## Implementation

With MSharp, adding `ReloadOnChange()` to the end of the search filter will cause the list to reload, whenever that filter's value gets updated.

```csharp
public EmployeesList()
{
    HeaderText("Employees");

    Search(x => x.Department).Control(ControlType.DropdownList).ReloadOnChange();

    Column(x => x.Name);
    Column(x => x.Department);
}
```
