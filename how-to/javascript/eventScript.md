# Running a script on an event

## Problem

You have some javascript code that you want to run when an event occured or the user performed an action, for example, you want to alter the look of the page without reloading it on a button click.

## Implementation

Add the javascript code using `Javascript` method to the event handler.

### Example
Suppose that we have a button on a form. Upon clicking, we want the button to simply hide itself before performing its other functions. For doing this, we add JavaScript code to the `OnClick` functionality of the button.

```csharp
    Button("Process").OnClick(x =>
    {
        x.Javascript(@"$(this).hide();");
        //other functionality
    });
```

This javascript is then generated in the Cshtml View by the above model code.

```csharp
<button type="button" name="Process" class="btn btn-secondary" onclick="$(this).hide();">Process</button>
```
If the code for the click handler merely contains JavaScript code, then no action method is generated in the controller.
