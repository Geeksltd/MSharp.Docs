# Calculated VS Persisted properties

When you define an entity in M#, it will create a column per property in the database.
These properties which are the default are called persisted properties and you usually use them to store some attribute of the entity.

There is another group of properties called calculated properties.
Calculated properties are not stored in the database and are used to return a value based on some business logic.
Calculated properties are read only and cause no database column to be created.

## Implementation

To mark some property as calculated, we call `Calculated()` method on the property using the fluent API.
Then we need to define the getter for the property to specify what business logic should be executed for the property using the `Getter()` method.

#### Example

Let's define an `Employee` entity and add a `FullName` property to it which returns the combination of the first and last names.

```csharp
using MSharp;

namespace Model
{
    public class Employee : EntityType
    {
        public Employee()
        {
            String("First name").Mandatory();
            String("Last name").Mandatory();
            String("Full name").Calculated().Getter("FirstName + ' ' + LastName");
        }

    }
}
```

As you can see, we define the C# expression for the `FullName` property as a string in the `Getter()` method.
The combination of `Calculated()` and `Getter()` will cause a read-only property to be created and also tells M# to not create a database column for the property.
#### Generated Code

```csharp
    public partial class Employee : GuidEntity
    {
        /// <summary>Gets or sets the value of FirstName on this Employee instance.</summary>
        public string FirstName { get; set; }
        
        /// <summary>Gets the FullName property.</summary>
        [Calculated]
        public string FullName
        {
            get => FirstName + ' ' + LastName;
        }
        
        /// <summary>Gets or sets the value of LastName on this Employee instance.</summary>
        public string LastName { get; set; }

protected override Task ValidateProperties()
        {
            var result = new List<string>();
            
            if (FirstName.IsEmpty())
                result.Add("First name cannot be empty.");
            
            if (FirstName?.Length > 200)
                result.Add("The provided First name is too long. A maximum of 200 characters is acceptable.");
            
            if (LastName.IsEmpty())
                result.Add("Last name cannot be empty.");
            
            if (LastName?.Length > 200)
                result.Add("The provided Last name is too long. A maximum of 200 characters is acceptable.");
            
            if (result.Any())
                throw new ValidationException(result.ToLinesString());
            
            return Task.CompletedTask;
        }
    }
```

As you can see, the definition of the `FullName` property is what we expect.
Also the validation method does not check anything in the `FullName` property since it is a read-only one and it doesn't make sense to check it for validity.

## Remarks

- Don't use properties for complex calculations since their callers don't expect it and might call them in an inappropriate way.
- Don't write complex logic in property's `Getter()` expression and define longer methods as a separate method and just call them in the `Getter()`.
- only very small properties (less than 32 CIL instructions), will be inlined, so try to make them as short as possible, specially if they will be called many times in loops and other hotspots.