# Custom display expression and format

## Problem

When creating a list, there will be times when you will want to explicitly define how you want a field in a list to look or what data to show.

## Implementation

In order to achieve this, we can use the methods `DisplayExpression()` and `DisplayFormat()`.

`DisplayExpression()` allows us to define the source of the data that will show in the list.  A common use for this is when you have a list where a column is an associated entity like `Status` for example. The column will show the name of the status by default and this may not be what you want the user to see. If you had a property in `Status` called `DisplayName` You could use `DisplayExpression("@item.DisplayName")` to show that property rather than the default name of the `Status`

`DisplayFormat()` allows us to define how the data will show to the user.  A common use would be when showing `DateTime` properties as different applications will want to format dates in different ways.  

## Example

```csharp
Column(x => x.Status).DisplayExpression("@item.Status.Alias");
```

```csharp
Column(x => x.StartDate).DisplayFormat("{0:d}");
```
