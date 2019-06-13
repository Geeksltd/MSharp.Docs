# Passing and using parameters

## Problem

In most applications, there will be times when you need to use parameters and pass them from one module to another.  

Whenever you need to edit an item in a list, you will need to pass the `item` when navigating to the form module in order to edit.

You also need to pass a parameter if the next page you are navigating to has modules that require information from your current module in order to show the right data to the user.

## Implementation

M# has a few methods we can use to do this.

- `Pass()` - You can pass the item by adding it into this method and this is passed in the query string.

- `Send()` - You can structure the query string more appropriately for your needs.

- `FromRequestParam()` - On the receiving module you can specify what parameter you need to call.

### Example

```csharp
using MSharp;

namespace Modules
{
    class AdminViewApplicationMenu : MenuModule
    {
        public AdminViewApplicationMenu()
        {
            IsViewComponent()
                  .RootCssClass("navbar")
                  .UlCssClass("nav");
            VisibleIf(AppRole.Adviser, AppRole.Admin);

            Item("Mortgage Application")
                .CssClass("has-submenu")
                .OnClick(x => x.Go<Admin.Applicants.MortgageApplicationPage>().Pass("application"));

            Item("Documentation")
                .CssClass("has-submenu")
                .OnClick(x => x.Go<Admin.Applicants.DocumentationPage>().Pass("application"));

            Item("Recommended Mortgages")
                .OnClick(x => x.Go<Admin.Applicants.ApplicantRecommendedMortgagesPage>().Pass("application"));

            Item("Solicitor Information")
                .OnClick(x => x.Go<Admin.Applicants.SolicitorPage>().Pass("application"));

            Item("Fees")
               .OnClick(x => x.Go<Admin.Applicants.FeesPage>().Pass("application"));

            Item("Application Tracker")
               .OnClick(x => x.Go <Admin.Applicants.ApplicationTrackerPage>().Pass("application"));

            Item("Case Notes")
             .OnClick(x => x.Go < Admin.Applicants.CaseNotesPage>().Pass("application"));
        }
    }
}
```

In this example, we have a menu module and we use `Pass()` to pass the `application`

```csharp
using MSharp;
using Domain;
namespace Modules
{
    class AdviserAddressDetailsList : BaseListModule<ApplicantAddress>
    {
        public AdviserAddressDetailsList() : base()
        {
            HeaderText("Address Details").Markup("[#BUTTONS(Edit_AddressDetails)#]");
            DataSource("await info.Application.Addresses?.GetList()");
            ViewModelProperty<MortgageApplication>("Application").FromRequestParam("application");
            EmptyMarkup("There are no addresses to display");
            Button("Edit").Name("Edit_AddressDetails").CssClass("pull-right")
                .OnClick(x =>
                {
                    x.If(AppRole.Adviser).Go<Adviser.ViewApplication.MortgageApplication.Edit_Application.AddressListViewPage>().Send("application", "info.Application.ID");
                    x.If(AppRole.Admin).Go<Admin.Applicants.MortgageApplication.Edit_Application.AddressListViewPage>().Send("application", "info.Application.ID");
                });

            Column(x => x.Status);
            CustomColumn("Address").DisplayExpression("@item.Address").LabelText("Address");
            Column(x => x.LivedInSince);
        }
    }
}
```

We then use the `FromRequestParam()` method passing the same `application` parameter meaning the correct information for this particular application is displayed.

Below we have an example of the `Send()` method and its versatility.

```csharp
using MSharp;

namespace Modules
{
    public class AdviserCoApplicantEmploymentHistoryList : BaseListModule<Domain.CoApplicantEmploymentHistory>
    {
        public AdviserCoApplicantEmploymentHistoryList() : base()
        {
            HeaderText("Co Applicant's Employment Details");
            DataSource("info.CoApplicant == null ? Enumerable.Empty<Domain.CoApplicantEmploymentHistory>() : await info.CoApplicant.GetEmploymentHistories()");
            EmptyMarkup("There is no employment history to display");
            VisibleIf("info.Application.IsJointApplicant");
            TableCssClass("cluttered-table");
            ViewModelProperty<Domain.MortgageApplication>("Application").FromRequestParam("application");
            ViewModelProperty<Domain.CoApplicant>("CoApplicant").OnBound("info.CoApplicant = await info.Application.CoApplicant;");

            Button("Edit").CssClass("pull-right")
                .OnClick(x =>
                {
                    x.If(AppRole.Adviser).Go<Adviser.ViewApplication.MortgageApplication.Edit_Application.CoAppEmploymentHistoryListPage>()
                    .Send("application", "info.Application.ID");
                    x.If(AppRole.Admin).Go<Admin.Applicants.MortgageApplication.Edit_Application.CoAppEmploymentHistoryListPage>()
                    .Send("application", "info.Application.ID");
                });

            ViewModelProperty<bool>("IsEmployed")
              .OnBound("listItem.IsEmployed = listItem.Item.EmploymentStatus.IsNoneOf(EmploymentStatus.Retired, EmploymentStatus.Un_employed);")
              .PerListItem();

            Column(x => x.IsCurrentEmployment).LabelText("Current employment").DisplayExpression("@(item.IsCurrentEmployment == true ? \"Yes\" : \"No\")");
            Column(x => x.StartDate).DisplayFormat("{0:d}");
            Column(x => x.EndDate).DisplayFormat("{0:d}").CellVisibleIf("@item.IsCurrentEmployment == false");
            Column(x => x.EmploymentStatus).DisplayExpression("@item.EmploymentStatus.Title");
            Column(x => x.EmployerName).LabelText("Employer/business name").CellVisibleIf("listItem.IsEmployed");
            CustomColumn()
            .LabelText("Address")
            .DisplayExpression("c#:item.Address").CellVisibleIf("listItem.IsEmployed");
            Column(x => x.Occupation).CellVisibleIf("listItem.IsEmployed");
            Column(x => x.Telephone).CellVisibleIf("listItem.IsEmployed");
            Column(x => x.NatureOfBusiness).CellVisibleIf("listItem.IsEmployed");
            Column(x => x.YearEstablished).CellVisibleIf("listItem.IsEmployed");
            Column(x => x.ShareOfBusiness).CellVisibleIf("listItem.IsEmployed");
            Column(x => x.OwningBusinessStartDate).CellVisibleIf("listItem.IsEmployed")
                .LabelText("Length of ownership")
                .DisplayExpression("c#:item.OwningBusinessStartDate.HasValue ? (LocalTime.Now - item.OwningBusinessStartDate.Value).ToCustomString(\"years\"):\"\"");
        }
    }
}
```

On the "Edit" button we are sending the parameter `application` again but this is not the item but a property on the item which we are able to define as `info.Application.ID`

#### Remarks

`SendReturnURL()` is another useful parameter passing method.  When a user needs to go back and forth between modules, this is a way to keep the information from the previous page to pass back to it when the user moves between the two.  

Be wary of "chaining" this method (especially when older browsers are in use by users) as the URL character limit can be easily hit.
