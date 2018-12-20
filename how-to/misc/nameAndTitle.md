# Name VS Title

## Problem

Sometimes the name you want to get generated for your entity property is different from what you want to display in UI modules.
You should not have to choose between them and go in great lengths to find something appropriate for both.
M# has the capability to choose them separately if needed.

## Implementation

When defining a property, you choose the display name of it which is the title and the entity name is derived from that as well.
Spaces are removed and it becomes a camel case property.
You can call the `Name()` method to set the C# generated name of the property and `Title()` method to set the name which is used in UI modules.

#### Example

Let's define a painting entity for a gallery which has the name of the painting with the cost it has been bought for and ...
We want to generate the name property as `Name` but shown in the UI as "Painting Name".

```csharp
using MSharp;

namespace Model
{
    public class Painting : EntityType
    {
        public Painting()
        {
            String("Painting Name").Mandatory().Name("Name");
            Int("Cost").CSharpTypeName("long");
            Date("Purchase date");
            Bool("Is bought").TrueText("bought").FalseText("donated").NullText("unknown");
        }
    }
}
```

The title property is set as display name in the `String()` method so we don't need to call `Title()` again unless we want to do it for readability.
The name is displayed in a form like this:

![painting form module](images/customTitle.PNG)

#### Generted code

The generated code of the painting class is listed here:

```csharp
    public partial class Painting : GuidEntity
    {
       /// <summary>Gets or sets the value of Cost on this Painting instance.</summary>
        public long? Cost { get; set; }
        
        /// <summary>Gets or sets a value indicating whether this Painting instance Is bought.</summary>
        public bool? IsBought { get; set; }
        
        /// <summary>Gets or sets the value of Name on this Painting instance.</summary>
        [System.ComponentModel.DisplayName("Painting Name")]
        public string Name { get; set; }
        
        /// <summary>Gets or sets the value of PurchaseDate on this Painting instance.</summary>
        [DateOnly]
        public DateTime? PurchaseDate { get; set; }
        
    }
```

As you can see the property is generated as `Name` but has a `[DisplayName]` attribute which tells the module system to show it with this display name.