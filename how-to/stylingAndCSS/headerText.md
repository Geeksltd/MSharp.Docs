# Header Text

## Problem

You want to change the header of a module, or add extra html to the top.

## Implementation

When applied to a Module .HeaderText() renders its contents within h2 tags. Designed for both static text and CSharp expressions.

```csharp
    public ViewAdmin()
    {
        HeaderText("@item Details")
            .Header("<p>An extra note about this page</p>");

        /*
        * other code
        */
    }
```

.Header() does not encase its contents in tags so it is more generalised. It is displayed after any HeaderText.

You can also use .HeaderText() to break up information within a form/view. Header text will appear above the field it is applied to. In this case it does not wrap the content in h2 tags thereby allowing you to customise the html.
