# Custom List Control Source

## Problem

In a form you have a ControlType with a list of options, you want to limit those options to those which are relevant.

For example, on an Employee form you have radio buttons to select office location, but you only want locations belonging to their Company to appear in this dropdown.

Or perhaps you have a dropdown with appointment slots, but you only want to display slots that are still available.

## Implementation

Using DataSource() you can control which options are available.

```csharp
    Field(x => x.PrimaryLocation)
        .AsRadioButtons(Arrange.Vertical)
        .DataSource("await Database.GetList<Location>().Where(x => x.CompanyId == info.Item.Company.ID)");

    Field(x => x.Appointment)
        .AsDropDown()
        .DataSource("await Appointment.GetUnbookedAppointments(info.Date)");
```

The controller uses async methods so await should be used.
