# Full text search

## Problem

In your application, you may want a search field that allows you to search all properties in a list rather than searching for a single property.  This gives the user.

## Implementation


We use the `Search()` method and pass `GeneralSearch.AllFields`.  This looks something like this in code.

```csharp
Search(GeneralSearch.AllFields).Label("Find");
```

The "Find" label is used as it makes the search field sound generic and the user will therefore understand the scope the search field has.

### Example

Below we have a list module that has the full text search

```csharp
using MSharp;

namespace Modules
{
    public class AdminApplicantsList : BaseListModule<Domain.MortgageApplication>
    {
        public AdminApplicantsList() : base()
        {
            HeaderText("Applicants").PageSize(10);
            EmptyMarkup("There are no applicants to display");

            ///================ Search: ================
            Search(GeneralSearch.AllFields).Label("Find:");

            Search(x => x.IsArchived).Label("Archived status")
              .Control(ControlType.HorizontalRadioButtons);

            SearchButton("Search").IsDefault()
                .OnClick(x => x.ReturnView());

            Button("@option.Item.Name").RepeatDataSource("info.Items");

            ///================ Columns: ================

            Column(x => x.Name);
            Column(x => x.Email);

            CustomColumn()
                .LabelText("Adviser")
                .DisplayExpression(@"c#:(await item.GetCurrentAdviser())?.Adviser.Name");

            ButtonColumn("Edit").HeaderText("Edit adviser").GridColumnCssClass("actions")
                .Icon("mz mz-edit").NoText()
                .VisibleIf(@"(item.Status.IsNoneOf(MortgageApplicationStatus.WaitingForApplicantToProceed,
                    MortgageApplicationStatus.WaitingForApplicantInformation,
                    MortgageApplicationStatus.WaitingForProductInformation))
                    && item.IsArchived == false")
                .OnClick(x => x.Go<Admin.Applicants.EditAdviserPage>().Send("application", "item.ID"));

            ButtonColumn("View").HeaderText("View Application").GridColumnCssClass("actions")
                .Icon("mz mz-view").NoText()
                .OnClick(x => x.Go<Admin.Applicants.ViewPage>().Send("application", "item.ID"));


            this.ArchiveButtonColumn("Applicant");
        }
    }
}
```

Below we see what happens when you search for any text within the list.  You can also do the same using this search for `Email` and `Adviser`

![applicantsList](images\applicantsList.PNG)
