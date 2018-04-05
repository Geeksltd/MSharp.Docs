# Database.Update()

In this lesson we will learn how to update and persist data. M# provides an `Update()` method to update records in the database. Each time an object is updated, the same events as for `Database.Save()` are raised: `Validate(), OnSaving()`.

### Overloads

There are four overloads for the Update method, one for updating one instance and the other for updating a list of instances.

```C#
namespace Olive.Entities
{
    public interface IDatabase
    {
        //... other methods

        Task<T> Update<T>(T item, Action<T> action) where T : IEntity;

        Task<T> Update<T>(T item, Action<T> action, SaveBehaviour behaviour) where T : IEntity;

        Task<List<T>> Update<T>(IEnumerable<T> items, Action<T> action) where T : IEntity;

        Task<List<T>> Update<T>(IEnumerable<T> items, Action<T> action, SaveBehaviour behaviour) where T : IEntity;

        //... other methods
    }
}
```

#### Examples

This overload allows you to update the properties of one entry.

```C#
public void Activate()
{
    Database.Update(this, x => x.IsAvtivated = true);
}
```

This overload allows you to update the properties of a list of entries in one line and inside a transaction scope. If one update fails all updates will be rolled back.

```C#
public void Activate(params IEnumerable<Employee> employees)
{
    Database.Update(employees, x => x.IsAvtivated = true);
}
```

#### Multiple properties

You can easily update many properties at the same time like this:

```C#
public void Activate()
{
    Database.Update(this, x => 
    {
        x.IsAvtivated = true,
        x.ActivationDate = LocalTime.Now
    });
}
```