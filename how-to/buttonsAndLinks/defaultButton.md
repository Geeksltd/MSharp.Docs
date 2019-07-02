# Default button

## Problem

Ideally, each page in your application should have a default button that the focus will start on. This will be predetermined as the most used button on that page and will therefore have input focus priority over other buttons on the page. This allows the user to press enter at any time and this will be the button that is pressed.

## Implementation

M# makes it easy to mark a button as default on a page by using the aptly named `IsDefault()` method.

### Example

This example shows how to use this method.

```csharp
SearchButton("Search")
    .IsDefault()
    .OnClick(x => x.ReturnView());
```

### Remarks

Be aware that you should only mark one button as `IsDefault()` per page.  Marking more than one default buttons renders the method unusable as you can not have two or more default buttons on one page.  It wont throw an error to notify you so be diligent when implementing this method.
