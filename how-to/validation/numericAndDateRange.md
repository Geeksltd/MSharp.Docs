# Numeric/Date ranges

## Problem

In many cases where you use a number or date, only some  ranges are acceptable and you should let the user know what range to enter and not allow him/her to enter values smaller or larger than the accepted range.

In M# you can define ranges for both `DateTime` and numeric (i.e. `Int()`, `Double()`, `Money()` and ...) properties.

## Implementation

To define minimum and maximum ranges for numeric types, you use the `Min()` and `Max()` methods.
You don't have to use both together of course.

For `DateTime`, `Date` and `Time` (which are all essentially `DateTime`) you can set the minimum and maximum acceptable ranges by using `LowerBound()` and `UpperBound()` methods.
These take a string which should be parsable to `DateTime` values using [`DateTime.Parse`](https://docs.microsoft.com/en-us/dotnet/api/system.datetime.parse?view=netframework-4.7.2).

#### Example

We want to define an `Employee` entity which has an age between 18 and 80 years old and a birthday between january first 1935 and january first 2000.
We define it like this

```csharp
using MSharp;

namespace Model
{
    public class Employee : EntityType
    {
        public Employee()
        {
            String("first Name").Mandatory();
            String("Last Name").Mandatory();
            Int("Age").Min(18).Max(80);
            Date("birthday").UpperBound("1/1/2000").LowerBound("1/1/1935");
        }
    }
}
```

As you can see we used `Min()` and `Max()` on the `Age` property and `UpperBound` and `LowerBound()` on the `Birthday` property.

#### Generated Code

The generated code contains validation code in the `ValidateProperties` method as well.

```csharp
public partial class Employee : GuidEntity
{
        /// <summary>Gets or sets the value of Age on this Employee instance.</summary>
        public int? Age { get; set; }
        
        /// <summary>Gets or sets the value of Birthday on this Employee instance.</summary>
        [System.ComponentModel.DisplayName("birthday")]
        [DateOnly]
        public DateTime? Birthday { get; set; }
        
        /// <summary>Gets or sets the value of FirstName on this Employee instance.</summary>
        [System.ComponentModel.DisplayName("first Name")]
        public string FirstName { get; set; }
        
        /// <summary>Gets or sets the value of LastName on this Employee instance.</summary>
        [System.ComponentModel.DisplayName("Last Name")]
        public string LastName { get; set; }
        
        /// <summary>
        /// Validates the data for the properties of this Employee and throws a ValidationException if an error is detected.<para/>
        /// </summary>
        protected override Task ValidateProperties()
        {
            var result = new List<string>();
            
            if (Age < 18)
                result.Add("The value of Age must be 18 or more.");
            
            if (Age > 80)
                result.Add("The value of Age must be 80 or less.");
            
            if (Birthday < DateTime.Parse("1/1/1935"))
                
            result.Add("The provided birthday is too early.");
            
            if (Birthday > DateTime.Parse("1/1/2000"))
                
            result.Add("The provided birthday is too late.");
            
            if (FirstName.IsEmpty())
                result.Add("first Name cannot be empty.");
            
            if (FirstName?.Length > 200)
                result.Add("The provided first Name is too long. A maximum of 200 characters is acceptable.");
            
            if (LastName.IsEmpty())
                result.Add("Last Name cannot be empty.");
            
            if (LastName?.Length > 200)
                result.Add("The provided Last Name is too long. A maximum of 200 characters is acceptable.");
            
            if (result.Any())
                throw new ValidationException(result.ToLinesString());
            
            return Task.CompletedTask;
        }
}
```

As you can see, the values are checked for their exact ranges, if they are not in the correct range, then an exception is thrown.