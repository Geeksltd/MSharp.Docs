# Hiding/showing buttons

## Problem

There will be times in your application where you will want to hide or show a button.  This will normally be down to either the user who is viewing that page with the button on or the stage or state of the application or properties.

## Implementation

We can do this in M# using the `VisibleIf()` method when adding a button to our module.  We can pass something into this method and this will create code that will set the reasoning for when this button should be visible.

### Example

Here we have an example of the `VisibleIf()` method being used.

```csharp
SearchButton("Search").VisibleIf(AppRole.Adviser)
                .OnClick(x => x.ReturnView());
```

In this example the "Search" button should only be visible if the current user has the `AppRole` of an "Adviser"

```csharp
Button("View Recommended Mortgage").VisibleIf("await CurrentApplication.GetCurrentRecommendedMortgage() != null")
                        .OnClick(x => x.Go<Applicant.Dashboard.ApplicantRecommendedMortgagePage>().Send("recommendedMortgage", "item.ID"));
```

In this example we have passed a boolean statement so that the button "View Recommended Mortgage" can only be seen if the current application has a recommended mortgage to view.

### Remarks

* The `VisibleIf()` method can also be used to control field visibility as well.
* Other methods such as `ColumnVisibleIf()` and `Visible()` methods are similar methods that can be used in other scenarios and work in a similar way.