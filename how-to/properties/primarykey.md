# Specifying the ID (primary key) property

## Problem

Each table in the database needs a primary key field.
Sometimes it is an additional (artificially created) property and sometimes one of the real properties of an entity can and should be used as the primary key.
The property can be of different types like string or number.
The primary key of an entity should be a unique value and you can find the entity using it in the database.

If you don't specify a primary key field when defining your entity, M# defines an additional `Guid` field named `ID` as the primary key of the entity in the database.
However M# allows you to choose one of your own properties as the primary key of the database.

## Implementation

The primary key can be of type: `Guid`, `int`, `long` or `string`.
If the primary key is not a `Guid` which is the default type, then you should call `PrimaryKeyType()` in your entity definition and set the type of the primary key.
Then you should simply call the `IsPrimaryKey()` method on the property and then M# will use this property instead of the usual ID property which it generates.

The `PrimaryKeyType()` method will accept a string parameter which is the type of the primary key.
The accepted values are:

- `"string"`
- `"long"`
- `"int"`
- `"Guid"`

#### Example

Let's say we have a `Product` entity with our own custom `ProductID` property which we want to set as the primary key.
The code will look like this

```csharp
using MSharp;


namespace Model
{
    public class Product :EntityType
    {
        public Product()
        {
            PrimaryKeyType("string");
            String("ProductID").Mandatory().IsPrimaryKey();
            Int("Cost").Mandatory();
            String("Product Name").Mandatory();
        }
    }
}
```

As you can see, we called `IsPrimaryKey()` on a mandatory `string` field.
Also we called `PrimaryKeyType()` and told the entity that we want it to have a string primary key.
Since a primary key cannot be null, the key should be a mandatory property, otherwise you'll get a build error when building the #Model project.

#### Generated Code

```csharp
public partial class Product : StringEntity
{
        /// <summary>Gets or sets the ID of this Product instance based on its ProductID property.</summary>
        public override string ID
        {
            get
            {
                return ProductID;
            }
            
            set
            {
                ProductID = value;
            }
        }
        
        /// <summary>Gets or sets the value of Cost on this Product instance.</summary>
        public int Cost { get; set; }
        
        /// <summary>Gets or sets the value of ProductID on this Product instance.</summary>
        [PrimaryKey]
        public string ProductID { get; set; }
        
        /// <summary>Gets or sets the value of ProductName on this Product instance.</summary>
        [System.ComponentModel.DisplayName("Product Name")]
        public string ProductName { get; set; }

}
```

There are multiple things to note in the generated code.
First of all, our `ProductId` property is marked with `[PrimaryKey]` attribute.
Secondly, the `ID` property is overridden to use the `ProductId` property as its underlying field.
Thirdly, the class is inherited from `StringEntity` instead of `GuidEntity`.

## Remarks

- If you have a property which you want to be your primary key and you need to query your database by it, then choose it as the primary key and don't waste memory and performance by letting M# choose its own primary key and then also creating an index for your other unique property.
- If you have a property which is unique and you want to be able to find your entity based on it, you can call `Unique()` on it and you don't have to make it your primary key.
you can set multiple properties as unique.
- The property which you set as primary key, should always call `Mandatory()` since otherwise it will be a nullable value which is not acceptable for a primary key
- When you set the type of the primary key as something other than `Guid`, then the entity will inherit from `IntEntity`, `StringEntity` and … based on key type.