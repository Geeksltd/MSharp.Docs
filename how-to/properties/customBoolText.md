# Custom Boolean text

## Problem

M# shows text values in the UI for bool values and sometimes you want something other than the default true and false values to be shown.
M# allows you to change the texts for true, false and null value (if the bool is nullable).

## Implementation

To set the custom text values you should use the fluent API on the `Bool()` property.
The methods are `TrueText()`, `FalseText()` and `NullText()`.

Let's say we have a painting entity which represents a painting in the gallery which can be either bought, donated or have an unknown status.
Let's say we want to show this state of the painting by a nullable bool value.

#### Example

```csharp
using MSharp;

namespace Model
{
    public class Painting : EntityType
    {
        public Painting()
        {
            String("Name").Mandatory();
            Int("Cost");
            Date("Purchase date");
            Bool("Is bought").TrueText("bought").FalseText("donated").NullText("unknown");
        }
    }
}
```

These custom texts doesn't affect the generated code or the database.
It only affects the texts displayed in the UI.

Now the property will be shown in the UI with your custom texts.

![custom bool text](images/customBoolText.PNG)