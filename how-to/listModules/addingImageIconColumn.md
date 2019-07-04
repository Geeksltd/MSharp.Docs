# Adding image/icon column

## Problem

Sometimes in your application, you will want to show a property in a table row as an icon or image.

## Implementation

In M# we can use the `ImageColumn()` method to add icons or images to the field in the table with the ability to set the width and height of this image in the model.

### Example

First, in the model we have an `OpenFile()` (you could also use `SecureFile()`)

property that can have its width and height set.

```csharp
OpenFile("Image").Width(20).Height(20);
```

Then in the UI we can reference this property like this.

```csharp
ImageColumn(x => x.Image)
```

This property in the table  will then use the width and height set in the model.  This simplifies the styling needed.
