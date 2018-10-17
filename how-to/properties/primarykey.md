# Specifying the ID (primary key) property

## Problem

Each table in the database needs a primary key field.
Sometimes it is an additional (artificially created) property and sometimes one of the real properties of an entity can and should be used as the primary key.
The primary key of an entity should be a unique value and you can find the entity using it in the database.

If you don't specify a primary key field when defining your entity, M# defines an additional `Guid` field named `ID` as the primary key of the entity in the database.
However M# allows you to choose one of your own properties as the primary key of the database.

## Implementation

The property which you want to assign as the primary key of your entity, should be of type `Guid`.
You should simply call the `IsPrimaryKey()` method on the property and then M# will use this property instead of the usual ID property which it generates.

#### Example

Let's say we have a `Product` entity with our own custom `ProductID` property which we want to set as the primary key.
The code will look like this

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
            Guid("MyProductId").Mandatory().IsPrimaryKey();
        }
    }
}

```

As you can see, we called `IsPrimaryKey()` on a mandatory `Guid` field.
That's because none-mandatory properties which are value types become nullable types (i.e. `Guid` becomes `Guid?`) and a primary key cannot be null.

#### Generated Code

```csharp
public partial class Product : GuidEntity
    {
        /// <summary>Gets or sets the ID of this Product instance based on its MyProductId property.</summary>
        public override Guid ID
        {
            get
            {
                return MyProductId;
            }
            
            set
            {
                MyProductId = value;
            }
        }
        
        /// <summary>Gets or sets the value of Cost on this Product instance.</summary>
        public int Cost { get; set; }
        
        /// <summary>Gets or sets the value of MyProductId on this Product instance.</summary>
        [PrimaryKey]
        [System.ComponentModel.DisplayName("MyProductId")]
        public Guid MyProductId { get; set; }
        
        /// <summary>Gets or sets the value of Name on this Product instance.</summary>
        public string Name { get; set; }

		...
        
        /// <summary>
        /// Validates the data for the properties of this Product and throws a ValidationException if an error is detected.<para/>
        /// </summary>
        protected override Task ValidateProperties()
        {
            var result = new List<string>();
            
            if (MyProductId == Guid.Empty)
                result.Add("MyProductId cannot be empty.");
            ...

            return Task.CompletedTask;
        }
    }
```

There are multiple things to note in the generated code.
First of all, our `ProductId` property is marked with `[PrimaryKey]` attribute.
Secondly, the `ID` property is overridden to use the `ProductId` property as its underlying field.
Thirdly, the validation code checks the `ProductId` property for being a none-empty `Guid`.

## Remarks

If you have a property which you want to be your primary key and you need to query your database by it, then choose it as the primary key and don't waste memory and performance by letting M# choose its own primary key and then also creating an index for your other unique property.