# Custom Search Element

## Problem

The client wants to Search by criteria not covered by the inbuilt Search functionality. For example, they want to search for Holidays with days between 2 date ranges.

## Implementation

A Holiday has a Start Date and an End Date. The search filter will have a field for Search Date From and Search Date To. The Client wants all Holidays that include any days between the search filters.

MSharps built in Search fields can only search one property, or all of them, at a time. Here you need to use 2 properties simultaneously. To do this you will need to create your own custom search field 

```csharp
CustomSearch("SearchDateFrom")
    .ViewModelName("SearchDateFrom")
    .ViewModelType("DateTime?")                
    .Label("Date")
    .AsDatePicker();

CustomSearch("SearchDateTo")
    .ViewModelName("SearchDateTo")
    .ViewModelType("DateTime?")               
    .Label("to")
    .AsDatePicker()
    .MemoryFilterCode(@"var searchDateFrom = info.SearchDateFrom ?? DateTime.MinValue;
                        var searchDateTo = info.SearchDateTo ?? DateTime.MaxValue;

                        if(searchDateFrom <= searchDateTo)
                        {
                            var searchRange = new Range<DateTime>(searchDateFrom, searchDateTo);
                            result = result.Where(x => new Range<DateTime>(x.StartDate, x.EndDate)
                                                        .Intersects(searchRange));
                        }");
```

- `CustomSearch()` – Make Search filters that do not depend on a property
- `ViewModelName()` and `ViewModelType()` - Add the search filters to the ViewModel. Generated in the controller as shown:

```csharp
namespace ViewModel
{
    [EscapeGCop("Auto generated code.")]
    #pragma warning disable
    public partial class HolidaysList : IViewModel
    {
        // Search filters
        public DateTime? SearchDateFrom { get; set; }
        public DateTime? SearchDateTo { get; set; }

        /*
        other properties
        */
    }
}
```

- `MemoryFilterCode()` - Insert the code to control the search functionality. Use `info.` to refer to the filter properties generated above. This code is also generated in the Controller, in the `GetSource()` method:

```csharp
async Task<IEnumerable<Gadget>> GetSource(vm.GadgetsList info)
{
    var query = Database.Of<Gadget>();
            
    var result = await query.GetList();

    var searchDateFrom = info.SearchDateFrom ?? DateTime.MinValue;
    var searchDateTo = info.SearchDateTo ?? DateTime.MaxValue;
            
    if(searchDateFrom <= searchDateTo)
    {
        var searchRange = new Range<DateTime>(searchDateFrom, searchDateTo);
        result = result.Where(x => new Range<DateTime>(x.StartDate, x.EndDate)
                                    .Intersects(searchRange));
    }
            
    return result;
}
```
