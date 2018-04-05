# Working with Existing Database

So far in the previous tutorials we have worked with managed entities *(Entities for which a database table is generated and mapped using the data access logic class)*. Sometimes we also need to work on an existing database and we just need to map the entity to a database table for data handling. In this tutorial, we will see how we can work with external databases in M#.

In tutorial [Entity, Page, Module](https://github.com/Geeksltd/MSharp.Docs/blob/master/Basics/Concepts.md), we discussed database modes while explaining entity management. Database mode is configurable at the time of creating an entity and also can be changed using entity attributes *(Please read tutorial [Understanding Entity Types](https://github.com/Geeksltd/MSharp.Docs/blob/master/Domain/UnderstandingEntityTypes.md) for more details on entity attributes)*.

When you need to deal with an existing database and want to generate ADO.NET data accessor but not the database table itself then you must select `DatabaseOption.Existing` in `DatabaseMode()` method after creating an entity in M#, as shown below:

```C#
using MSharp;

namespace Domain
{
    public class BankDetail : EntityType
    {
        public BankDetail()
        {
            DatabaseMode(DatabaseOption.Existing);

            String("Name");
        }
    }
}
```

by calling `DatabaseMode(DatabaseOption.Existing);`, M# generates the entity classes and ADO.Net data accessor, as for a managed entity but no database table is generated.

M# generates the Partial entity class and allows developers to generate the partial logic class for writing business rules *(Please read tutorial [Partial Classes & Business Logic](https://github.com/Geeksltd/MSharp.Docs/blob/master/Domain/PartialClass.md) for more details on working with partial classes)*.

M# also generates a data access logic (DAL) class for the created entity to map properties to the database columns enabling data access functionality.

> **Important:** Persisted properties of this type of entity must match the existing database table columns, because M# generates data access logic and maps properties to database columns.

If you want to create an entity without ADO.NET accessor you should call `DatabaseMode(DatabaseOption.Custom);`, as shown below:

```C#
using MSharp;

namespace Domain
{
    public class BankDetail : EntityType
    {
        public BankDetail()
        {
            DatabaseMode(DatabaseOption.Custom);

            String("Name");
        }
    }
}
```

For custom database mode type entities you must write your data access logic. You should only use this database mode when you need to communicate with an external database. If you do not have an external database and want to create an entity to perform complex business logic then you should consider **Transient** entity types *(Transient entities are explained more in tutorial [Transient, Abstract, Interface](https://github.com/Geeksltd/MSharp.Docs/blob/master/Domain/Transient.md))*.