# Custom search element

## Problem

There are times when creating a list module, where you will want to search for items that are a little deeper than just the properties of the class the module is based on.  

## Implementation

M# has a `CustomSearch()` method that we can use to create a search that has a more complicated nature than a standard `Search()`.  

### Example

Here is a good example of when a `CustomSearch()` is needed.  This is a search field to search which user has made a change on an assignment.

```csharp
 CustomSearch("Change user").Label("Change user")
                .ListItemValueExpression("item.ID")
                .ListItemTextExpression("item.Name").ViewModelType("User")
                .DataSource("await Domain.User.GetAll()").AsAutoComplete()
                .MemoryFilterCode(@"
                    if (info.ChangeUser != null)
                        result = await result.Where(async x => await x.ChangeHistory.Where(w => w.CreatedBy == info.ChangeUser).Any());

                    if (info.LastChanged != null || info.LastChangedMax != null)
                    {
                        var changedAfter = await result.Where(async x => await x.ChangeHistory.Where(w => w.CreatedAt > info.LastChanged).Any());
                        var changedBefore = await result.Where(async x => await x.ChangeHistory.Where(w => w.CreatedAt < info.LastChangedMax).Any());

                        result = changedAfter.Concat(changedBefore).Distinct();
                    }"),
```

The list module is on `Assignment`, but we need access to the `User` in order to know who made a change.  We can set the `ViewModelType` of this search to `User` and set the `DataSource()` to be the users in the database and further refine the search data be adding logic using `MemoryFilterCode()` to filter out which users are part of our search "pool".
