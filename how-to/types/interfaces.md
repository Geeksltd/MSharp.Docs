# Creating and using Interface types

## Problem:

An interface is a set of functionality which a class can implement.
For example if you want to provide export behavior in your software and multiple classes can export their data, you usually create an interface named `IExportable` which indicates all methods and properties which a class should implement to export its data.

In languages like C# which structs cannot inherit from other structs and multiple inheritance is not allowed for classes, interfaces play an important role.
Also if used well, interfaces can help you avoid creating deep and complex inheritance hierarchies which are hard to modify and maintain.
For these reasons M# allows you to use the power and flexibility of the interfaces with ease.

## How to implement

In order to indicate an entity is an interface, you should define its `DatabaseMode` as `Transient` and also call the `IsInterface()` method in its public constructor.

#### Example

Let's say in our shopping application we have multiple types of items which can be sold and they should have two properties: `HasFreeShipping` and `Discount` which show if the product has free shipping and if it has any discounts applied or not. 
The discount will be an integer which should be between 0 and 100 (if the shop keeper is sane, probably between 0 and at most 75).
We don't complicate our example by defining the range but we define the `ISellable` interface which can be used for this purpose.

```csharp
using MSharp;

namespace Model
{
    public class ISellable : EntityType
    {
        public ISellable()
        {
            DatabaseMode(DatabaseOption.Transient);
            IsInterface();
            Bool("HasFreeShipping").Mandatory();
            Int("Discount").Mandatory();
        }
    }
}
```

As you can see our entity definition doesn't have much difference with ordinary entities.
It is transient which means it will not be stored in a database table and also it is an interface so other entities can implement it.

Now if we want to implement the interface by our `product` class, we need to define all elements of the interface in our `Product` public constructor and also should call `Implements()` method in the public constructor as well.
The code would be like this

```csharp
using MSharp;

namespace Model
{
    public class Product : EntityType
    {
        public Product()
        {
            Implements("ISellable");

            Bool("HasFreeShipping").Mandatory();
            Int("Discount").Mandatory();
            String("Name").Mandatory();
            Int("Cost").Mandatory();
        }
    }
}

```

Now the `Product` class will implement the `ISellable` interface and we can pass it to any method or generic class which requires an instance of type `ISellable`

#### Generated Code

Let's take a look at the generated code for `ISellable` first.

```csharp
public partial interface ISellable : IEntity<Guid>
    {
         /// <summary>Gets or sets the value of Discount on this Sellable instance.</summary>
        int Discount { get; set; }
        
        /// <summary>Gets or sets a value indicating whether this Sellable instance is HasFreeShipping.</summary>
        [System.ComponentModel.DisplayName("HasFreeShipping")]
        bool HasFreeShipping { get; set; }
    }
```

As expected it is an interface instead of a class deriving from any other entity base type.

The code for product is like this

```csharp
    public partial class Product : GuidEntity, ISellable
    {
       /// <summary>Gets or sets the value of Cost on this Product instance.</summary>
        public int Cost { get; set; }
        
        /// <summary>Gets or sets the value of Discount on this Product instance.</summary>
        public int Discount { get; set; }
        
        /// <summary>Gets or sets a value indicating whether this Product instance is HasFreeShipping.</summary>
        [System.ComponentModel.DisplayName("HasFreeShipping")]
        public bool HasFreeShipping { get; set; }
        
        /// <summary>Gets or sets the value of Name on this Product instance.</summary>
        public string Name { get; set; }
        ...
    }
```
As you can see the class implements the `ISellable` interface correctly.

## Remarks

- An entity which want to define an interface should be transient but none-transient entities can implement interfaces.
- Interfaces can help you make your code modular with easy to understand conceptual models and inheritance hierarchies
- Use interfaces when the entity itself doesn't need to implement any functionality instead of defining an abstract class.