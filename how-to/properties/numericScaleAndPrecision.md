# Numeric scale/precision

## Problem

M# has multiple numeric data-types.
You can use

- `Int()`: defines an `int` property
- `Decimal()`: defines a `decimal` property
- `Double()`: defines a `double` property.
- `Money()`: defines a `decimal` property which is a currency as well
- `Percent()`: defines a `decimal` property which is a percent between 0 and 100

And each of them have different characteristics.
The important thing we want to talk about here are scale and precision.

### Precision

Precision is the number of digits at the left and right side of the decimal point combined.
So a number with precision of 10 can have at most 10 digits.
If it has 7 digits at the left side of the decimal point, the right side can have at most 3 digits and if the left side has 6 digits then the right side can have up to 4 digits.

### Scale

Scale of each number is defined as the minimum number of digits that you want to have at the right side of the decimal point.
If you have a double of scale 2 then the numeric type is SQL Server will be Numeric(27,2).
It means that the left side of the decimal point will store at most 25 digits and always reserves at least 2 digits for the right side of the decimal point.

#### Example

You can use the `Scale()` method to set the scale of a numberic property.
If you want to always have 3 digits after the decimal point to store millimeter accurate data, then you need to define your `Position` entity like this.

```csharp
using MSharp;

namespace Model
{
    public class Position : EntityType
    {
        public Position()
        {
            Double("X").Mandatory().Scale(3);
            Double("Y").Mandatory().Scale(3);
            Double("Z").Mandatory().Scale(3);
        }
    }
}
```
This will make sure that any stored value will always have enough precision at the right side of the decimal point.

## Remarks

- Scale is only meaningful for `double` and `decimal` types in C# so setting scale on an `int` property will make it a double but this is not recommended, define what you intent clearly to avoid surprizes.
