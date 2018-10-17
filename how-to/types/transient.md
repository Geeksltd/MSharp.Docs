# Implementing transient (non DB) types

## Problem:

Sometimes you'll need to define entities which are not stored in the database.
These entities might be used as DTOs to pass data between your domains or in any other place in your custom logic.
M# could leave you to define them as classes in pure C# yourself but that's a waste of time and effort when you have M#.

## How to implement

Each M# entity can have one of different **database modes**.
It can be of typed **Managed** which is the default and will cause the entity to be stored in the database and creates a SQL table for it.
It can be **transient** which means it is not stored in the database and no SQL table is created for it.
It can also have a couple of other database modes for the time that you want to use a custom database table or use an existing one which are not related to transient entities and will not be discussed here.

To set the database mode of an entity , we use the `DatabaseMode()` method which takes an argument of type `DatabaseOption`.
A transient entity should set its option to `DatabaseOption.Transient` and as said the default option is `DatabaseOption.Managed` which is what you usually want for your defined entities.

#### Example

Let's say we want to define an entity called `CustomerDeliveryData` which contains customer's address and other related data for the delivery of goods to them.
We use this entity to pass data to our delivery application and not to store customer info in the database so it should be a transient one.
Still we choose to define it in M# so it can generate validation, cloning and all other methods for us.

```csharp
using MSharp;

namespace Model
{
    public class CustomerAddressData : EntityType
    {
        public CustomerAddressData()
        {
            DatabaseMode(DatabaseOption.Transient);
            String("CustomerName").Mandatory();
            String("DeliveryInfo").Mandatory();
            String("Address").Mandatory();
            Int("AcceptableHoursStart").Mandatory();
            Int("AcceptableHoursEnd").Mandatory();
        }
    }
}
```
As you can see we define the database mode of the entity in the first line of the public constructor as transient by calling this `DatabaseMode(DatabaseOption.Transient)`.

#### Generated code

The generated code of the entity is pretty similar to managed (default) entities other than an important attribute which you'll see.

```csharp
    [TransientEntity]
    [EscapeGCop("Auto generated code.")]
    public partial class CustomerAddressData : GuidEntity
    {
       /// <summary>Gets or sets the value of AcceptableHoursEnd on this Customer address data instance.</summary>
        [System.ComponentModel.DisplayName("AcceptableHoursEnd")]
        public int AcceptableHoursEnd { get; set; }
        
        /// <summary>Gets or sets the value of AcceptableHoursStart on this Customer address data instance.</summary>
        [System.ComponentModel.DisplayName("AcceptableHoursStart")]
        public int AcceptableHoursStart { get; set; }
        
        /// <summary>Gets or sets the value of Address on this Customer address data instance.</summary>
        public string Address { get; set; }
        
        /// <summary>Gets or sets the value of CustomerName on this Customer address data instance.</summary>
        [System.ComponentModel.DisplayName("CustomerName")]
        public string CustomerName { get; set; }
        
        /// <summary>Gets or sets the value of DeliveryInfo on this Customer address data instance.</summary>
        [System.ComponentModel.DisplayName("DeliveryInfo")]
        public string DeliveryInfo { get; set; }
    }
```

As you can see the entity's generated code has an attribute of type `[TransientEntity]` which tells the other systems in M# that this is a transient entity and they don't need to generate any storage related code, database table or … for it.

## Remarks

- Any time you need a class for any usage which doesn't need to be stored in the database, it should be a transient entity
- Transient entities are marked with `[TransientEntity]` attribute to tell other parts of M# that this entity is transient, otherwise it has no difference in class hierarchy and other properties.
- Transient entities aren't much heavier performance-wise at all compared to plain classes, so don't worry about them and use them freely.
