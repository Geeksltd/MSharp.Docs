# Search Field on Property

## Problem

Sometimes you want to fill the search filter by default values. For example you want to only show the active items in the list and hide the archive items.

## Implementation

Using `DefaultValueExpression()` allows you to set the default value on your serch filter.

```csharp
 Search(x => x.IsArchived).Label("State:").Control(ControlType.HorizontalRadioButtons).DefaultValueExpression("false");
```



