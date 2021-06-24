# Auto-search on start

## Problem

The client wants to have control over the results populated in a list when the list is shown for the first time. It is often desired to show lists which has a huge number of records. Showing all the results could take longer to bind the data grid. In this case, the client gets the results based on the search criteria or some initial filtering being applied to the result set in a situation where pre-set search elements exist.

## Implementation

M# has a `StartUpBehaviour` attribute in Lists that you can utilize to set the preferred start-up behaviour of the list. This affects how the result set will be loaded for the first time. This attribute takes an enum type of `OnStart`.

`OnStart` can have the following values:

- `LoadList`: List will be populated based on the specified data source. This is the default startup behaviour, so in this case, you can skip the entire attribute.
- `AutoSearch`: List will be populated based on the specified data source but the data source will be filtered based on the search elements default set values.
- `WaitForSearch`: List will not be populated unless a postback happens on the page.

For example, you display product catalogues with options to filter products. You need to display products based on the default set filters e.g. Most Reviewed, Most Rated etc. In this case, you can use the `AutoSearch` option to automatically filter the result set initially. When the list is shown for the first time, only the most rated product catalogues are shown.

```csharp
public ProductCataloguesList()
{
    StartUpBehaviour(OnStart.AutoSearch);

    Search(x => x.Filter).Control(ControlType.HorizontalRadioButtons).DefaultValueExpression("MostRated");

    SearchButton("Search").OnClick(x => x.Reload());

    //...
}
```

As another example, you need to display a batch of payments which needs to be verified at the month-end which has a huge number of records. Showing all the results is not desired here. In this case, you can use `WaitForSearch` to display only the records which need to be managed by their status. Initially, the list will be empty till the client select the status and press the `Search` button.

```csharp
public PaymentsList()
{
    StartUpBehaviour(OnStart.WaitForSearch);

    Search(x => x.Status).Control(ControlType.DropdownList);

    SearchButton("Search").OnClick(x => x.Reload());

    //...
}
```
`StartUpBehaviour` attribute can also be chained to `HeaderText` as follows: 
```csharp
public AgenciesList()
{
    HeaderText("Agencies")
        .ShowHeaderRow()
        .Sortable()
        .PageSize("20")
        .DataSource("ArchivedItemService.GetAllItems<Agency>()")
        .StartUpBehaviour(OnStart.AutoSearch);

    //...
}
```