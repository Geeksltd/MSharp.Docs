# Pagination

## Problem

Your list has a lot of entries and you only want to display a set number of them to avoid long loading times and an infinite scroll bar

## Implementation

You can limit the number of records that appear on a page using PageSize(). If you want the user to be able to change the number of records per page you can include a PageSizeSelector(), you can choose if this appears at the top and/or bottom of the page.

MSharp will automatically produce a page selector so the user can browse through the records. If you wish you can include PagerPosition() to specify where this page selector will appear.

```csharp
    public ContactsList()
    {
        HeaderText("Contacts");

        PageSize(5);
        PageSizeSelector(PagerAt.Top);
        PagerPosition(PagerAt.TopAndBottom);

        Column(x => x.Name);
        Column(x => x.Phone);
        Column(x => x.Email);

        ButtonColumn("Edit"). Icon(FA.Edit)
            .OnClick(x=> x.PopUp<Contact.EnterPage>().Send("item", "item.ID"));

        Button("New Contact").Icon(FA.Plus)
            .OnClick(x => x.PopUp<Contact.EnterPage>());
    }
```
