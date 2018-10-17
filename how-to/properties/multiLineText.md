# Multiline text

Sometimes the text input of the user is longer than a single word or sentence.
Usually you want to show a multiline text field in those situations.
M# makes it easily possible to do this in the fluent API.

## Implementation

You need to simply call the `Lines()` method on the ``String` property to let the M# UI know that you want a multiline text area control for the property.
This has no effect neither on the database column's type nor on the generated class.

#### Example

Let's define a `Description` property for a product class and set it to show a multiline text area as UI.

```csharp
using MSharp;

namespace Model
{
    public class Product : EntityType
    {
        public Product()
        {
            String("Name").Mandatory();
            Int("Cost").Mandatory();
            String("Description").Lines(5);
        }
    }
}
```

Now when you want to add a product or edit one, the description field will be a text area.

![multiline text image](images/multilineText.png)

And M# did this without any hints from us when creating the `EnterProductModule`