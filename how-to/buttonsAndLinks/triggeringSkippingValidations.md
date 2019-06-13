# Triggering/skipping validations

## Problem

There will be times in an application that you want action events to cause an error in the application and other times when you will want the application to skip the validations that would catch this error.

## Implementation

We can use the `CausesValidation()` method to explicitly decide wether a validation should be triggered or skipped.  By default this is set to true.

### Example

```csharp
 Button("Confirm")
    .CausesValidation()
    .OnClick(x =>
    {
        x.CSharp("await UserRegistrationService.ApproveAdviser(info.Item);");
        x.CloseModalAndRefereshParent();
        x.GentleMessage("Saved successfully.");
    });
```
