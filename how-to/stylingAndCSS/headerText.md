# Header text

## Problem

You want to be able to create consistent header texts throughout your application.

## Implementation

In M# we have the `HeaderText()` method that we use to set the header for a module.

### Example

We can pass a simple `string`

```csharp
HeaderText("Reports")
```

Or we can also pass logic.

```csharp
HeaderText("@item.GetActiveReport().FirstOrDefault().Name")
```
