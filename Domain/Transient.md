# Transient, Interface, Abstract
In this lesson, we will have a look at transient, Interface and abstract type implementation using M#.

## Transient
Transient by definition is something short-lived or in other words is limited to certain tasks. In M#, transient entities have same meaning in terms of data. M# allows developers to create transient entities, which do not have any mapping to the database. M# does not create a SQL table for the entity marked as transient, but marks such transient entities with `[TransientEntity]` attribute. Transient entities usually are used to process some intermediary data or to perform any required business logic which needs to be encapsulated in separate business object /entity.

### Creating Transient Entity
Navigate to the **#Model** project and create a **Domain** folder, *right click > Add > M#* and then add **Payment** class:

```C#
using MSharp;

namespace Domain
{
    public class Payment : EntityType
    {
        public Payment()
        {
            DatabaseMode(DatabaseOption.Transient);

            String("Title");
        }
    }
}
```

M# creates an entity class in C# but no database table is created at this time, as shown in below:

```C#
/// <summary>Represents an instance of Payment entity type.</summary>
[TransientEntity]
[EscapeGCop("Auto generated code.")]
public partial class Payment : GuidEntity
{
    /* -------------------------- Properties -------------------------*/
        
    /// <summary>Gets or sets the value of Title on this Payment instance.</summary>
    public string Title { get; set; }
        
    /* -------------------------- Methods ----------------------------*/
        
    /// <summary>Returns a textual representation of this Payment.</summary>
    public override string ToString() => Title.OrEmpty();
        
    /// <summary>
    /// Validates the data for the properties of this Payment and throws a ValidationException if an error is detected.<para/>
    /// </summary>
    protected override Task ValidateProperties()
    {
        var result = new List<string>();
            
        if (Title?.Length > 200)
            result.Add("The provided Title is too long. A maximum of 200 characters is acceptable.");
            
        if (result.Any())
            throw new ValidationException(result.ToLinesString());
            
        return Task.CompletedTask;
    }
}
```
> **Note:** This class has a attibute name **`[TransientEntity]`**.

## Interfaces
Interfaces in any programing language accumulate definitions of core related functionalities that a class or structure can implement. This is very important feature especially in .Net programing languages like C# where multiple inheritance is not allowed. For Stuct type, it is even more essential, because a struct cannot inherit from another Struct type.

### Creating interfaces
M# allows developers to create Interface types, which can be later be used in Logic partial class of any entity. You can create interfaces using the same process as mentioned above while creating a Transient entity:

```C#
using MSharp;

namespace Domain
{
    public class Payment : EntityType
    {
        public Payment()
        {
            DatabaseMode(DatabaseOption.Transient);

            IsInterface();

            String("Title");
        }
    }
}
```
> **Note:** Only transient entity can be Interface

## Abstracts
Abstraction is about encapsulating core concepts but leaving out the concreteness and implementation for specific scenarios, which could be extended later. In Object-Oriented Programing an abstract class contains the core functionalities (definitions or general implementation) for any business logic, which is then inherited and extended as required by derived classes because abstract classes cannot be instantiated and must be inherited in order to consume those core functionalities.

As a developer you can mark any class "Abstract" as required by your business logic. M# allows developers to make any type of entity as Abstract e.g. Transient, Managed etc.

In our tutorial, a good contender for abstraction could be the "User" entity. User contains few properties, which are inherited by "Employee" and will be validated to login and perform actions on our website. So, User entity has no specific or direct interaction with the system, meaning we can mark it as an "Abstract" class.

```C#
using MSharp;

namespace Domain
{
    public class User : EntityType
    {
        public User()
        {
            Abstract();

            String("First name").Mandatory();
            String("Last name").Mandatory();
            String("Name").Calculated().Getter("FirstName + \" \" + LastName");
            String("Email", 100).Mandatory().Unique().Accepts(TextPattern.EmailAddress);
            String("Password", 100).HashPassword().SaltProperty("Salt").Accepts(TextPattern.Password);
            String("Salt");
            Bool("Is deactivated").Mandatory();
        }
    }
}
```

```C#
using MSharp;

namespace Domain
{
    public class Employee : SubType<User>
    {
        public Employee()
        {
            String("Code").Mandatory();
        }
    }
}
```