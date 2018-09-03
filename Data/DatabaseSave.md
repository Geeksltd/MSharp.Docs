# Database.Save()

In this lesson, we will learn about possible ways to persist an entity instance in the database. M# offers `Databas.Save()` method for this purpose. M#'s provided data persistence facility is not only limited to single entity instance but is also available for persisting a collection of records. M# provides six overloads of `Database.Save` method. In this lesson, we will work with the *Employee* entity and will see how we can call `Database.Save` on an entity instance(s).

> **Note:** `Database.Save` also returns the saved instance(s) to be used later in code.

## Overloads

```csharp
namespace Olive.Entities
{
    public interface IDatabase
    {
        //... other methods

        Task<T> Save<T>(T entity) where T : IEntity;

        Task Save(IEntity entity, SaveBehaviour behaviour);

        Task<IEnumerable<T>> Save<T>(T[] records) where T : IEntity;
        
        Task<IEnumerable<T>> Save<T>(List<T> records) where T : IEntity;

        Task<IEnumerable<T>> Save<T>(IEnumerable<T> records) where T : IEntity;

        Task<IEnumerable<T>> Save<T>(IEnumerable<T> records, SaveBehaviour behaviour) where T : IEntity;

        //... other methods
    }
}
```

### Examples

#### Saving a New Employee Instance

```csharp

await Database.Save(new Employee
        {
            FirstName = "John",
            LastName = "Wills",
            Password = "*******",
            Email = "John.Wills@uat.co"
        });
```
The code above demonstrates that we are saving a new instance of *Employee* entity.

#### Saving an Array of Employees

M# runs bulk saves in **Transaction**. Meaning, failure to save one records results rolling back all the saved instances of the current collection.

```csharp
await Database.Save(new Employee[]{
            new Employee{FirstName = "John",LastName="Wills",Email="john.wills@uat.co",Password = "******"},
            new Employee{FirstName = "James",LastName="Wills",Email="james.wills@uat.co",Password = "******"}
        });
```

#### Saving a Single Employee by Specifying Save Behaviour

```csharp
await Database.Save(
            new Employee{FirstName = "John",LastName="Wills",Email="john.wills@uat.co",Password = "******"},
            SaveBehaviour.BypassSaved);
```
The code above shows that we are saving a new record of *Employee*, but also supplying an additional parameter **SaveBehaviour**. The additional parameter is used in special cases when you want to omit any event in the pipeline of the `Database.Save()` method. **SaveBehaviour** enum and save pipeline is discussed later in this chapter.

#### Saving a List of Employees by Specifying Save Behaviour

```csharp
await Database.Save(new Employee[]{
            new Employee{FirstName = "John",LastName="Wills",Email="john.wills@uat.co",Password = "******"},
            new Employee{FirstName = "James",LastName="Wills",Email="james.wills@uat.co",Password = "******"}
        }, SaveBehaviour.BypassSaved);
```
The code shown above is saving a List of Employees by specifying **SaveBehaviour**.

> **Important:** `Database.Save()` can also be used to update an existing record. Although, it is not recommended to call `Database.Save()` method for updating an existing entity instance, but in exceptional cases, always `Clone()` the entity instance before changing and then call `Database.Save()` by passing cloned object. The reason is that you are changing the object that is already referenced on data cache so If Save action fails the object on cache would be different than the one in database. (Memory Cache is not transactional). M# offers another method `Database.Update()` to update existing records, which should be used always and is discussed in next lesson.

## Events Raised During Database.Save()

Whenever an entity instance is saved or updated, it goes through a series of events, which are used to implement core business logic e.g. validation. M# allows developers to override these events in the Logic partial class of an entity.

> For more information on Partial classes, please read lesson [Partial Classes and Business Logic](https://github.com/Geeksltd/MSharp.Docs/blob/master/Domain/PartialClass.md).

Below are the events overridden in Logic class of an entity:

```csharp
public override Task Validate()
{
    // validate core business logic
    //e.g. validation dependant on roles
    return base.Validate();
}
``

```csharp
protected override Task OnSaving(CancelEventArgs e)
{
    if (IsNew)
    {
        // Perform any pre-saving business logic. Fires just before a new instance is saved
    }
    else
    {
        // Perform any pre-saving business logic. Fire just befor an existing record is being updated
    }

    return base.OnSaving(e);
}
```

## Save Behaviour Enum
M# provides `Database.Save()` method overloads with an extra parameter of an enum type `SaveBehaviour`. This enum type is used to bypass the events raised (Shown above ) while saving an entity instance as required in the business logic, below is the code of the enum options:

```csharp
namespace Olive.Entities
{
    [Flags]
    public enum SaveBehaviour
    {
        Default = 1,
        BypassValidation = 2,
        BypassSaving = 4,
        BypassSaved = 8,
        BypassLogging = 16,
        BypassAll = 30
    }
}
```

For example, if you want to supress the `BypassValidation` event of an entity when you save an entity instance then you should use the `SaveBehaviour.BypassValidation` enum option, as shown in below code:

```csharp
await Database.Save<Employee>(new Employee
        {
            FirstName = "John",
            LastName = "Wills"
        }, SaveBehaviour.BypassValidation);
```