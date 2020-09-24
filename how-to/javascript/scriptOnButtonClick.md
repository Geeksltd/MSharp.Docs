# Script to Run on Button Click

## Problem

You have some javascript that you want to run when the User clicks a button, for example, you want to alter the look of the page without reloading it.

## Implementation

Add the javascript code to the OnClick functionality of the button.

This button simply hides itself before performing its other functions.

```csharp
    Button("Process").OnClick(x =>
    {
        x.Javascript(@"$(this).hide();");
        //other button functionality
    });
```

This javascript is then generated in the Cshtml View

```csharp
<button type="button" name="Process" class="btn btn-secondary" onclick="$(this).hide();">Process</button>
```
