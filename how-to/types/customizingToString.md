# Customizing ToString() implementation

## problem

The `ToString()` method in .NET is very important. It is used to get a textual representation of your class.
You might use it for display purposes or debugging.

M# has its own uses for `ToString()` as well.
For example it uses the value of `ToString()` when searching for entities or showing their name in a drop-down.
M# should allow you to define how an entity's `ToString()` is implemented.

## Implementation

To provide a new implementation for the `ToString()` method, you should call the `ToStringExpression()` method in your entity's public constructor.
The string argument of the `ToStringExpression()` can be any valid C# code but if the code is complex, you can define a function for it and just call the function here.

#### Example

Let's define a `ToString()` method for an employee with a first name and a last name.

```csharp
using MSharp;

namespace Model
{
    public class Employee : EntityType
    {
        public Employee()
        {
            String("FirstName").Mandatory();
            String("LastName").Mandatory();
            ToStringExpression("$\"{FirstName} {LastName} \"");
        }
    }
}

```

Now the `ToString()` should return full name of the employee.
#### Generated Code

```csharp
    public partial class Employee : GuidEntity
    {
        
        /// <summary>Gets or sets the value of FirstName on this Employee instance.</summary>
        [System.ComponentModel.DisplayName("FirstName")]
        public string FirstName { get; set; }
        
        /// <summary>Gets or sets the value of LastName on this Employee instance.</summary>
        [System.ComponentModel.DisplayName("LastName")]
        public string LastName { get; set; }
        
        /// <summary>Returns a textual representation of this Employee.</summary>
        public override string ToString() => $"{FirstName} {LastName} ";

    }
```
As you can see, our exact expression is copied to the implementation of the `ToString()` method.

## Remarks

- As said before, if the `ToString()` method is something complex, you can define a utility method for it and just call it in the `ToStringExpression()` method.
To define the utility method you should create a partial class with the name of your entity class in the `Logic` directory of your Domain project.
- Avoid allocating too many strings in the `ToString()` method.
- Keep in mind that strings in .NET are immutable and any modification to them means allocating new string objects.
- Use `StringBuilder` if you have to do lots of string manipulation.
- Don't use `StringBuilder` for a few small modifications since the cost of creating it and getting the string from it will be heavier than just allocating a few strings. Just like everything else, use your profiler to see if it's an issue or not.