# Hiding Header Row

## Problem

You want to hide the header row

## Implementation

The header row contains the column headings.

You can remove individual Column headings using NoLabelText()
```csharp
    Column(x => x.Category);
    Column(x => x.WeightInKg);
    Column(x => x.Description).NoLabelText();
```
However, if you want to hide the entire header row, use ShowHeaderRow(false)
```csharp
    public ProductList()
    {
        HeaderText("Products")
            .ShowHeaderRow(false);

		/*
        *other code
        */
    }
```
