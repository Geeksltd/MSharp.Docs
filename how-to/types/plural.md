# Customizing plural title

Sometimes you want a different plural name instead of the automatically generated ones.
The plural name is used both in UI and in the database table names.
M# allows you to customize the value of the plural name of an entity.

## Implementation

There is a  method called `PluralName()` which can call in the public constructor to set a custom plural title.

#### Example

We want to set `Employee`'s plural name to `"Staff"`.
We should write a code like this.

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
            PluralName("Staff");
        }

    }
}
```

M# will follow the instruction and will use this name at any place it needs to make the employee name plural like the database table name.

![plural name in the DB](images/plural.png)