# User Column Display Selection

## Problem

A List has many columns that negatively impacts usability. The Client wants the User to be able to select which columns are visible.

## Implementation

Each Column can be given a `DisplayMode()`. If at least one column has a Display Mode other than default, a selector becomes available allowing the User to show or hide the columns.

There are 4 Display Modes available

-	Always – The column is always displayed and the User can not hide it
-	Default – The column is initially visible but can be hidden
-	Selectable – The column is initially hidden but the User can make it visible
-	Never – The column is always hidden and the User cannot make it visible

```csharp
    Column(x => x.ID);
    Column(x => x.Name).DisplayMode(DisplayMode.Always);
    Column(x => x.IsActive);
    Column(x => x.Address).DisplayMode(DisplayMode.Selectable);
    Column(x => x.Contacts).DisplayMode(DisplayMode.Selectable);
```
