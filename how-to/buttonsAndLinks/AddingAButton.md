# Adding A Button

## Problem

You need to add a button to a module to allow a user to be able to click this button to perform an action.

## Implementation

The `Button()` method can be used to create a button in the UI.

You can then set various things such as the text on the button as well as the behaviour of the button when clicked.

### Example

```csharp
Button("Save")
```

In this example we have created a "Save" button.

We can then apply other methods in MSharp to make the button behave the way we want it to.

```csharp
 Button("Save").IsDefault()
            .OnClick(x =>
            {
                x.SaveInDatabase();
                x.GentleMessage("Saved successfully.");
                x.Go<Admin.CMS.Home.TestimonialsPage>();
            });
```
