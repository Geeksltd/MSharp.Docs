# Mutually exclusive

## Problem

Sometimes there might be a need to set a value for only one mutual property, for instance, consider `LargDescription` and `ShortDescription` as a mutual property that one of them must be filled by the end users and by filling one of them the other one should be set `null`.

## Implementation

By overriding `.Validate()` method we can add our custom validation process, here in this example we should check `LargDescription` and  `ShortDescription` value and if they are not filled by the user we should throw an exception and if `LargDescription` is set we should set `ShortDescription` value `null` and vice versa.

#### Example

Let's say we have a product entity that has a name, short and large description property. the name property is mandatory and one of the large or short property must be entered by the user.

```csharp
using MSharp;

namespace Domain
{
    class Product : EntityType
    {
        public Product()
        {
            String("Name").Mandatory();
            String("Short description");
            BigString("Larg description");
        }
    }
}

```

Before saving process we should check _short_ and _large_ property value and add our arbitrary logic.

```csharp
namespace Domain
{
    public partial class Product
    {
        public override Task Validate()
        {
            var result = new List<string>();

            if (LargDescription.IsEmpty() && ShortDescription.IsEmpty())
                throw new ValidationException("Please enter large or short description");

            if (!LargDescription.IsEmpty())
                ShortDescription = string.Empty;

            if (!ShortDescription.IsEmpty())
                LargDescription = string.Empty;

            return base.Validate();
        }
    }
}
```

As you can see, by overriding `.Validate()` method we are able to add our arbitrary logic there and we are sure that all saved data are efficient.