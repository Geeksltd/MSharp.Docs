# Custom form elements

## Problems

Sometimes when creating a form module, you will want to add a field that is a property of a different entity to the data source of the form module itself or even create a property that is only used in this one instance.

## Implementation

We can use the `CustomField()` method to tailor an element to what we need for the application to work as expected.

If we are creating a new property then we can set the `PropertyName` and `PropertyType` of the field.

### Examples

Here we have an example of a field that is creating a property that adds a boolean field to this module.

```csharp
 CustomField()
    .Label("Please confirm that your circumstances have not changed")
    .PropertyName("HasConfirmedNoChange").PropertyType("bool")
    .Control(ControlType.CheckBox);
```

In this example we see a whole module with some elements using a `ViewModelProperty<T>` as the data source.

```csharp
using Domain;
using MSharp;

namespace Modules
{
    public class RecommendedMortgagesReportDetailsView : ViewModule<Domain.MortgageApplication>
    {
        public RecommendedMortgagesReportDetailsView()
        {
            IsViewComponent();

            SecurityChecks(@"User.IsInRole(""Admin"") || 
                            (User.IsInRole(""Adviser"") && info.RecommendedMortgage.SelectedBy == User) ||
                             info.Application.Applicant == CurrentApplicantUser || info.CoApplicant?.Applicant == CurrentApplicantUser");
            DataSource("info.Application");
            RootCssClass("recommended-mortgages-report-details-view");

            ///================ View model properties: ================

            ViewModelProperty<ApplicationRecommendedMortgage>("RecommendedMortgage").FromRequestParam("recommendedmortgage");
            ViewModelProperty<MortgageApplication>("Application").OnBound("info.Application = info.RecommendedMortgage.Application;");
            ViewModelProperty<CoApplicant>("CoApplicant").OnBound("info.CoApplicant = await info.Application.CoApplicant;");


            ///================ Fields: ================
            Box("Applicant Details", BoxTemplate.WrapperDiv)
                .ContainerLayout("<h2>Applicant Details</h2>[#GROUP#]").Add(
                Field(x => x.Title),
                Field(x => x.FirstNames),
                Field(x => x.LastName),
                Field(x => x.DateOfBirth).DisplayFormat("{0:d}")
            );
            Box("Co-Applicant Details", BoxTemplate.WrapperDiv).Visibility("info.Application.IsJointApplicant == true && info.CoApplicant != null")
                .ContainerLayout("<h2>Co-Applicant Details</h2>[#GROUP#]").Add(
                CustomField().LabelText("Title").DisplayExpression("@info.CoApplicant.Title"),
                CustomField().LabelText("First names").DisplayExpression("@info.CoApplicant.FirstName"),
                CustomField().LabelText("Last name").DisplayExpression("@info.CoApplicant.LastName"),
                CustomField().LabelText("Last name").DisplayExpression(@"@info.CoApplicant.DateOfBirth.ToString(""d"")")
            );
        }
    }
}
```