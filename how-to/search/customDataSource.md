# Custom data source

## Problem

There will be times when creating an application where you will want to use a custom search filter element to search for particular properties that are sub categories of the list.

## Implementation

We can provide a custom data source for the search filter element by using the `DataSource()` method.  We can then then explicitly state which properties we wish the filter element to search for by passing a `string` through this method.

### Example

```csharp
CustomSearch()
    .Label("Lease end Date")
    .AsDropdown()
    .ViewModelType("int?")
    .ViewModelName("LeaseAgreementRange")
    .DataSource("GetDateRanges()");
```

In this example of a custom search, we are passing another method that decides the data source for this search.  `GetDateRanges()` provides a list of options for the dropdown.
