# Adding Input Control Column

## Problem

You want to be able to edit list items in a list module

## Implementation

To add input control to a column you need to do two things:

1.	Make the column editable by giving it a control type using one of the AsXxx() methods.

2.	Save the changes to the Database once the User has finished editing.

In this example, the Phone Number column has been rendered AsTextbox() and a Save button column has been added which allows the User to update individual records.

```csharp
    public ContactsList()
    {
        HeaderText("Contacts");

        Column(x => x.Name);
        Column(x => x.Phone).AsTextbox();
        Column(x => x.Email);

        ButtonColumn("Save")
            .NoHeaderText()
            .GridColumnCssClass("actions")
            .Icon(FA.Save)
            .OnClick(x => {
                x.CSharp("item.UpdatePhone(info.Items.First(x=> x.Item.ID == item.ID).Phone);");
                x.Reload();
            });
    }
```

 > - item is the original list item as pulled from the database
 > - info contains the changes made to the form elements

In the Domain a method, UpdatePhone(), has been added to the partial class Contact:
```csharp
    partial class Contact
    {
        public Task UpdatePhone(string newNumber)
        {
            return Database.Update(this, x => x.Phone = newNumber);
        }
    }
```
