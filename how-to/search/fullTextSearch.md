# Full Text Search

## Problem

If you have many text fields in a List that you want to filter by you may find that you have too many search fields making the search space look overly complicated.

Or maybe you have several similar fields that it would be meaningless to distinguish between, i.e. Home Number and Work Number.

## Implementation

With MSharp you can search all fields by text.

Simply `Search()` using `GeneralSearch.AllFields`. There is no default label, so it is recommended that you add one.

```csharp
public ContactsList()
{
    HeaderText("Contacts");

    Search(GeneralSearch.AllFields).Label("Find:");

    SearchButton("Search").OnClick(x => x.Reload());

    Column(x => x.Name);
    Column(x => x.Alias);
    Column(x => x.Email);
}
```
