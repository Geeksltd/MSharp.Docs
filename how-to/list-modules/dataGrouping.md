# Data Grouping

## Problem

You want to group List Data into separate tables.

For example, in an Employee List you may want to display a separate table of Employees per Department.

## Implementation

Use Grouping() and specify the item property to group by.

You can add as many Groupings as you like. When you apply a Grouping to a list module, MSharp generates a grouping drop down that allows the User to select a grouping or no grouping. This example has 4 available Groupings.

```csharp
    public EmployeeList()
    {
        HeaderText("Employees")

        Grouping(x => x.Department)
            .Title("Sector")
            .IsDefault();
        Grouping(x => x.Status)
            .GroupTemplate(@"<div>[#HEADER#]<div class=""some-class"">[#ITEMS#]</div></div>");
        Grouping(x => x.Office)
            .DisplayExpression("<h3>Location: @group.Key.Location</h3>");
        Grouping("Unauthorised Holiday Days")
            .ValueExpression("item.TimeOff.Unauthorised.Count()");

        /*
        * other code
        */
    }
```

There are several Methods available to customise your Groupings

- IsDefault() – The Grouping this is applied to will be the default, applied on first loading the page, if there is no default specified the default grouping will be no grouping
- Title – This is the text that is displayed in the dropdown list to refer to this grouping
- DisplayExpression() – Customise the header for each grouping, can be different for each grouping
- ValueExpression – For if the grouping Key is more complex than an item property. Grouping should be invoked using  a Title string instead of a Linq statement.
- GroupTemplate - You can fully customise the html of your groupings. You can use placeholders [#HEADER#] and [#ITEMS#]. Only use once, it will apply to them all.
