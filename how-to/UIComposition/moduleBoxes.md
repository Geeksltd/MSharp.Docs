# Module boxes

## Problem

Sometimes in your application, it would be useful to be able to wrap some of your content together when creating a module.  This allows you to manipulate this the way that you want to, keeping the wrapped items together.

## Implementation

M# has the `Box()` method where we can cleanly create a wrapper for the contents.

### Example

We can create a variable that represents a box

```csharp
var preferredProductBox = Box("Your Preferred Product", BoxTemplate.HeaderBox)
```

We can give this box a css class that we can refer to when it comes to styling the application.

```csharp
var preferredProductBox = Box("Your Preferred Product", BoxTemplate.HeaderBox)
    .CssClass("preferred-product-box")
```

We can then add items to this box using the `Add()` method.

```csharp
 preferredProductBox.Add(
                Field(x => x.IsFixedProduct).Mandatory()
                    .Label("Would you prefer a fixed or variable product?")
                    .TrueText("Fixed")
                    .FalseText("Variable")
                    .Control(ControlType.HorizontalRadioButtons),

                 Field(x => x.FixedProductLength).Mandatory()
                    .Label("How long would you like to fix your rate?")
                    .Control(ControlType.HorizontalRadioButtons),

                Field(x => x.VariableProductLength).Mandatory()
                    .Label("How long would you like to protect your introductory rate?")
                    .Control(ControlType.HorizontalRadioButtons));
```
