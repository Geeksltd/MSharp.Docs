# Sorting

## Problem

You want to determine the order of a List module

## Implementation

A List can be easily sorted using a SortingStatement().
- Input csharp expressions using the “item” object
- Use | to separate additional sorting statements
- Use DESC to specify a descending order
```csharp
    public ProductList()
    {
        HeaderText("Products")
            .SortingStatement("item.Category DESC | item.WeightInKg");

        /*
        *   other code
        */
```

In this example, Products are sorted by Category in reverse alphabetical order and then by Weight.

This causes the following code to be generated in the GetSource method of the controller

```csharp
    result = result.OrderByDescending(item => item.Category)
                   .ThenBy(item => item.WeightInKg);
```
