# Calculated properties
Property defines the structure of an entity and usually holds values. M# allows developers to create two types of properties, which are explained below.

**Calculated properties** are created for read-only purposes and returns data based on business requirements. M# defines these types of properties in **Entity Class** of the **#Model** project and marks them with **Calculated** method. No SQL table Column is created for such properties. A calculated property is usually used to display some information on UI or in decision making. A good example of this could be to have a "Full Name" property on "Employee" entity, as shown in the code below.

```C#
using MSharp;

namespace Domain
{
    public class Employee : EntityType
    {
        public Employee()
        {
            String("First name");

            String("Last name");

            String("Full name").Calculated().Getter("FirstName + LastName");
        }
    }
}
```

```C#
/// <summary>Gets the FullName property.</summary>
[Calculated]
public string FullName
{
    get => FirstName + LastName;
}
```

Having such calculated properties allows developers to write more concrete code, eliminating the redundancy of code and making it easier to manage changes.

FOR EXAMPLE: In above scenario, if you do not use a calculated property and concatenate the First and Last Name of Member on different modules or pages instead, If at a later date you need to show "Middle Name" in "Full Name" of member , it will be much more difficult and time consuming to change it on each module rather simply updating the Calculated Property.
 

> **Note:** A calculated property must not contain complex calculations because this is not the intended purpose of entity behaviours. It is always recommended to implement Methods / Functions for such complex calculations.