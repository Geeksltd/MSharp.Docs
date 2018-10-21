# Custom primary key

## Problem

By default M# generates a `Guid` field named ID and uses it as the primary key of the entity.
Sometimes your entity by default has a property which is unique per touple and can be used as primary key.
M# allows you to choose a `Guid` as the primary key.

## Implementation

You should call the `IsPrimaryKey()` method on a property to set it as the primary key of your entity.

#### Example

Each employee in our company has a unique employee ID used for identifying him.
We can use this ID as the primary key of the employee in the database.
In order to do that, we define our employee like the code below:

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
            Guid("EmployeeIdentifier").Mandatory().IsPrimaryKey();
        }
    }
}

```

The employee ID property which we have here is calling `IsPrimaryKey()` in its chain so the M# framework will choose this property as primary key.

#### Database Schema

The database schema will look like this

![custom primary key](images/pk.PNG)

#### Generated Code

The generated code for the `Employee` entity will accommodate changes so it uses the custom ID.

```csharp
    public partial class Employee : GuidEntity
    {
        /* -------------------------- Properties -------------------------*/
        
        /// <summary>Gets or sets the ID of this Employee instance based on its EmployeeIdentifier property.</summary>
        public override Guid ID
        {
            get
            {
                return EmployeeIdentifier;
            }
            
            set
            {
                EmployeeIdentifier = value;
            }
        }
        
        /// <summary>Gets or sets the value of EmployeeIdentifier on this Employee instance.</summary>
        [PrimaryKey]
        [System.ComponentModel.DisplayName("EmployeeIdentifier")]
        public Guid EmployeeIdentifier { get; set; }
        
        /// <summary>Gets or sets the value of FirstName on this Employee instance.</summary>
        [System.ComponentModel.DisplayName("first Name")]
        public string FirstName { get; set; }
        
        /// <summary>Gets or sets the value of LastName on this Employee instance.</summary>
        [System.ComponentModel.DisplayName("Last Name")]
        public string LastName { get; set; }
    }
```

The `Employee` code overrides the `ID` property so it uses the custom ID property we have, usually entity classes don't need to override this and use the `GuidEntity`'s implementation.