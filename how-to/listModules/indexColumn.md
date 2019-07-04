# Index column

## Problem

Sometimes, it is useful to know what index a particular row has in a list.

## Implementation

We have the method of `IndexColumn()` that allows us to quickly implement a column, marking the index of a row.

### Example

Here, we see the index column method implemented for a list of admin users.

```csharp
using MSharp;

namespace Modules
{
    public class AdminUsersList : BaseListModule<Domain.AdminUser>
    {
        public AdminUsersList() : base()
        {
            IndexColumn(true);
            HeaderText("Admin users");
            ///================ Search: ================
            Search(GeneralSearch.AllFields).Label("Find:");

            Search(x => x.IsArchived).Label("Archived status")
              .Control(ControlType.HorizontalRadioButtons);

            SearchButton("Search")
                .OnClick(x => x.ReturnView());

            ///================ Columns: ================
            Column(x => x.Name);
            Column(x => x.Email);

            LinkColumn("Reset password").HeaderText("Reset password")
                .OnClick(x => x.CSharp("await PasswordResetService.RequestTicket(item);"))
                .ConfirmQuestion("Are you sure you want to reset password for this user?");

            ButtonColumn("Edit").HeaderText("Edit").GridColumnCssClass("actions")
                .Icon("mz mz-edit").NoText()
               .OnClick(x => x.Go<Admin.Settings.AdminUsers.EnterPage>().Send("item", "item.ID"));

            this.ArchiveButtonColumn("Admin user").CellVisibleIf("item != CurrentAdminUser");

            ///================ Buttons: ================
            Button("New Admin user").IsDefault()
                .OnClick(x => x.Go<Admin.Settings.AdminUsers.EnterPage>());
        }
    }
}
```

This will show in the UI on the left hand side of the list as follows.

![index column](images\indexColumn.PNG)
