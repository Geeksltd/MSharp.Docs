# Associations
M# allows you to quickly create different types of associations between your entities with a clean SQL schema and generated C# code. It also gives you flexibility by using some specific Association attributes allowing you to change the behaviour in your C# logic or the generated SQL code.

### Creation
Create a new entity for which you want to create an association with, for example `Status`.

```csharp
using MSharp;

namespace Domain
{
    public class Status : EntityType
    {
        public Status()
        {
            String("Name");
        }
    }
}
```

Create another new entity which will have association, for example `Employee` and create association using generic `Associate` method:

```csharp
using MSharp;

namespace Domain
{
    public class Employee : SubType<User>
    {
        public Employee()
        {

            String("Name");

            Associate<Status>("Status");
        }
    }
}
```

M# will generate following code:

```csharp
/// <summary>Gets or sets the value of Status on this Employee instance.</summary>
public Status Status
{
    get => cachedStatus.Get(StatusId);
    set => StatusId = value?.ID;
}
```

## Methods

| Methods     | Sample     | Description      |
|:------------|:-----------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------|
| .MinCardinality(int value)             | `Associate<Status>("Status") .MinCardinality(2);`     | Min cardinality will have no effect on the database column definition. M# will generate a new validation rule to make sure that your instance has at least two statuses. |
| .MaxCardinality(int? value)            | `Associate<Status>("Status") .MaxCardinality(5);` | Max cardinality will have no effect on the database column definition. M# will generate a new validation rule to make sure that your instance has not more than five statuses. |
| .OnDelete(CascadeAction value)         | `Associate<Status>("Status") .OnDelete(CascadeAction.CascadeDelete);` | This attribute allows you to define a specific action when the associated instance is deleted. `Throw warning: `This is the default behaviour of the association, the Status cannot be deleted if it is associated to an Employee and a ValidationException is thrown. `Cascade delete:`If the Status is deleted all employees with this status will also be deleted. `Set to null:`If the Status is deleted all employees associated to this Status will have a null status. `Call ReleaseXXX method:`This will allow you to have the full control on the behaviour, in our example you will have to create the method: `public void ReleaseStatus()`. |

> **Note** : In some scenarios, you may have `InverseAssociate()` on another side of the relationship and in this case, you should use `MinCardinality()` and `MaxCardinality()` only in the inverse side after `InverseAssociate()`.
