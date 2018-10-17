# Adding custom methods

## Problem

In more complex applications, you need to add custom behavior to your entities.
Also sometimes the code you need to write for a calculated property or custom implementation of `ToString()` or Display Expression is complex and is not convenient to be done in a string literal.
String literals are not testable either.

For all these reasons, M# should allow you to easily add custom code to generated entities.

## Implementation

The `partial` keyword in C# is exactly created for this and has always been used for this purpose by Visual Studio itself and other tools and frameworks.
Specifying some class as partial means that, this code is only part of the class's code and the rest of it can be defined in other places.
The compiler simply combines all the content of these classes when trying to compile the application.

M# generates all of its entities as partial classes.
Each entity gives you the opportunity to add custom methods to it.
In order to do this you should define your own partial class with the same name of the entity class and put it in the Logic folder of the **Domain** project.

#### Example

Let's say we want to define a custom `ToString()` method for a class representing customer addresses and this `ToString` method is complex.
We choose to define it as a method called `CustomToString()` and just call this in our `ToString()` implementation.

The entity will look like this.

```csharp
using MSharp;

namespace Model
{
    public class CustomerAddressData : EntityType
    {
        public CustomerAddressData()
        {
            String("CustomerName").Mandatory();
            String("DeliveryInfo").Mandatory();
            String("Address").Mandatory();
            Int("AcceptableHoursStart").Mandatory();
            Int("AcceptableHoursEnd").Mandatory();
            ToStringExpression("CustomToString()");
        }
    }
}

```

Now the generated `ToString()` method will try to call `CustomToString()` like this

```csharp
public override string ToString() => CustomToString();
```
As you know, our `CustomerAddressData` entity doesn't have such method so after building #Model project, your Domain project will have a compile error due to this.
Now we should create a partial class in the `Logic` folder and call it `CustomerAddressData` and define it like this

```csharp
namespace Domain
{
    public partial class CustomerAddressData
    {
        private string CustomToString()
        {
            string myAddress = Address;
            if (string.IsNullOrEmpty(Address))
                myAddress = "undefined";
            return $"Customer: {CustomerName} Address: {myAddress}";

        }
    }
}
```

The logic we put on `CustomToString()` here doesn't matter for now. But let's assume we want to show undefined for empty addresses in `ToString()`
The way I've done it here, it can be tested and when writing it you have all IDE features at your finger-tips.
Also sometimes you need much more involved logic which need to be written to be used side-by-side of the M# generated code, this feature makes you capable of writing it easily and cleanly.

## Remarks

- The partial keyword doesn't do any magical merging of your definitions and will just concatenate the content of the all partial classes with the same name.
- The generated entity code in []GEN-Entities] is overridden at each #Model project build, don't add any code to it. Add all of your logic to the Logics folder of the Domain project.