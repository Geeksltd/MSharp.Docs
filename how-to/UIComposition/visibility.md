# Visibility

## Problem

Sometimes in an application, you want to be able to control the visibility of certain items on a page either due to the current state of certain entities or properties or the permissions of the user who is viewing that page.  Having the ability to do this reduces development time as modules can be re-used with the visibility rules defining what each user sees at any time.

## Implementation

We can manipulate the visibility of many different things such as headers, tabs, list columns or even entire modules using methods in M#.

### `VisibleIf()`

This method can be used in several situations such as when you are creating menu items that should only be seen by certain users in the system or if you have a field on a module that should only be seen in certain situations.  You can pass your criterion for the visibility (examples below).

### `Visibility()`

This method works in the same way but this is primarily used for settting the visibility for boxes (example below).

### Examples

Below we have a menu that has visibility rules depending upon what AppRole the user has.

```csharp
using MSharp;

namespace Modules
{
    public class AdminMainMenu : MenuModule
    {
        public AdminMainMenu()
        {
            AjaxRedirect().WrapInForm(false);
            IsViewComponent().UlCssClass("nav navbar-nav dropped-submenu");

            Item("Admin Applications")
                .VisibleIf(AppRole.Admin);

            Item("Applicant Applications")
                .VisibleIf(AppRole.Applicant)
                .CssClass("visible-in-collapsed-only");
        }
    }
}
```

In this example we have a widget that has been broken down into boxes where the visibility of each box is dependant upon certain logic being true in order for a box to be visible using the `Visibility()` method. It also has visibility rules on the fields within these boxes using `VisibleIf()` showing the versatility of these methods.

```csharp
namespace Modules
{
    public class ApplicantNextAppointmentWidget : ViewModule<Domain.Appointment>
    {
        public ApplicantNextAppointmentWidget()
        {

            DataSource("await CurrentApplication.GetNextAppointment()");
            HeaderText("Next Appointment");
            IsViewComponent(true);
            RootCssClass("dashboard-box");

            Box("emptyBox", BoxTemplate.WrapperDiv)
              .Visibility("await CurrentApplication.GetNextAppointment() == null")
              .Add(
                 CustomField().CssClass("no-label-control").DisplayExpression(@"You currently have no appointment. 
                        Your appointments with your assigned adviser will appear here when you have an adviser assigned."));

            Box("visbileBox", BoxTemplate.WrapperDiv)
                .Visibility("await CurrentApplication.GetNextAppointment() != null").Add(

                Field(x => x.AppointmentOn).LabelText("Date").DisplayFormat("{0:d}"),
                Field(x => x.AppointmentOn).LabelText("Time").DisplayFormat("{0:hh:mm tt}"),
                CustomField().LabelText("Location").DisplayExpression("@item.Adviser.FirmAddress"),
                Field(x => x.Method).DisplayExpression("@item.Method.Text"),
                Field(x => x.Status).DisplayExpression("@item.Status.Text"));

            Button("View Appointments").VisibleIf("await CurrentApplication.Appointments.Any()")
                        .OnClick(x => x.Go<Applicant.Dashboard.ApplicantAppointmentsPage>());

            Button("Request Appointment")
              .VisibleIf(@" await CurrentApplication.GetCurrentAcceptedAdviser() != null &&
                            await CurrentApplication.Appointments.None()")
              .OnClick(x => x.Go<Applicant.Dashboard.ApplicantRequestAppointmentPage>()
              .Target(OpenIn.PopupWindow));
        }
    }
}
```