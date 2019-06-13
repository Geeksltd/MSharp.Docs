# Custom validation message

## Problem

By default, a mandatory field will display a validation message with the syntax "The [FieldName] field is required.".

Sometimes you need to be able to define the validation message in your code to make it more user friendly in the UI.

## Implementation

We can use the `.RequiredValidationMessage()` method to amend this.  By passing a string in this method we can override the default validation message with our own.

### Example

```csharp
 Field(x => x.HasExistingMortgage
                .Control(ControlType.HorizontalRadioButtons)
                .Label("Do you have any existing mortgages?")
                .Mandatory();
```

This field, if not filled out by the user on save, will show the validation message "The Has existing mortgage field is required.".

```csharp
Field(x => x.HasExistingMortgage)
                .Control(ControlType.HorizontalRadioButtons)
                .Label("Do you have any existing mortgages?")
                .RequiredValidationMessage("The existing mortgage field is required.")
                .Mandatory();
```

Now the validation message will show "The existing mortgage field is required." which is much more user friendly.
