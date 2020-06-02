# Nullable (int, bool ...)

## Problem

Structs and built-in data-types in C# other than string cannot take a `null` value and are value types.
Sometimes you need to have a value which can have either a built-in type or a null value.
For this purpose, the .NET and C# teams at Microsoft created the nullable value types.
In C# you can either use the short form of the type which is `type-name?` like `int?` or `bool?` or the long form which is `Nullable<T>` like `Nullable<int>`.

You should be able to define these in M# as well.

## Implementation

Any none-mandatory type defined as an entity property which is a value type like `int`, `Guid`, `bool`, `double` and … will be defined as a nullable property by the code generator.
So if you don't call `Mandatory()` on a property of a value type, it will be nullable.

#### Example

Let's define an entity to represent paintings in a gallery.
Each item will have a name, an optional purchase date and another optional purchase cost.
Some of them are not purchased and are either donated or inherited which we set their purchase date and cost to null.

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
        }
    }
}
```

#### Generated Code

```csharp
public partial class Painting : GuidEntity
    {
       /// <summary>Gets or sets the value of Cost on this Painting instance.</summary>
        public int? Cost { get; set; }
        
        /// <summary>Gets or sets the value of Name on this Painting instance.</summary>
        public string Name { get; set; }
        
        /// <summary>Gets or sets the value of PurchaseDate on this Painting instance.</summary>
        [DateOnly]
        public DateTime? PurchaseDate { get; set; }
        
    }
```

In the generated code, nullable types are defined with the `?` character and unlike the mandatory properties can take null values when inserted/modified.