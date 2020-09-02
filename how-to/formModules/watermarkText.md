# Watermark Text

## Problem

You want to make the expected format of a text field more explicit without making the labels of your form too long.

## Implementation

Watermarks display placeholder text in empty text fields.

Watermarks are implemented using the WatermarkText() method which supports both text and C# expressions.

```csharp
    Field(x => x.DateOfPurchase).WatermarkText("dd/mm/yyyy");
    Field(x => x.ModelNumber)
        .WatermarkText("c#: info.IsOldModel ? \"eg. RH-G235\" : \"eg. RHG-2957\"");

```

 Watermarks are frequently used alongside labelling to avoid the UI getting too visually cluttered. However, as the text disappears when the user writes in the field it can be unwise to use watermarks instead of labels.
