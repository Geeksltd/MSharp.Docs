# Database.Get()

In this lesson, we will discuss two methods within M# Data access repository. These methods are used to fetch a single table record from the database. For this lesson we will use our **Employee** entity, which inherits the **User** entity, to discuss these methods in detail.

## Database.Get() 

This method has four overloads, requires an "Entity Type" to retrieve a record from and an *ID* to identify the record. This method returns single instance of the provided Entity Type and throws *System.ArgumentNullException*, if the input parameter is `null` or `empty`.

> **Note:** The Entity Type must implement the "IEntity" Interface. (For more information in M# Interface, please read lesson [IEntity Interface](https://github.com/Geeksltd/MSharp.Docs/blob/master/Domain/Advanced/IEntityInterface.md), in chapter 3.)

Below are the codes of the seven overloads for this method:

```C#
namespace Olive.Entities
{
    public interface IDatabase
    {
        //... other methods

        Task<T> Get<T>(string entityId) where T : IEntity;

        Task<T> Get<T>(int id) where T : IEntity<int>;  
  
        Task<T> Get<T>(int? id) where T : IEntity<int>;  
  
        Task<T> Get<T>(Guid id) where T : IEntity;  
  
        Task<T> Get<T>(Guid? id) where T : IEntity;

        Task<IEntity> Get(object entityID, Type objectType);

        Task<IEntity<Guid>> Get(Guid entityID, Type objectType);

        //... other methods
    }
}
```

This method must only be used when single record is required from database based on the *ID* of the entity. This method also boosts performance because M# runs the query in SQL environment.